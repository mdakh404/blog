---
title: Getting access to 25000 employees details
description: 'Hi guys,'
date: '2017-11-08T17:07:12.924Z'
categories: []
keywords: []
slug: /@ehsahil/getting-access-to-25k-employees-details-c085d18b73f0
---

Hi guys,

I want to share one of my findings in a private program on HackerOne, which was — critical but straightforward one. During testing for that private program. I found an endpoint for Internal team management.

![Internal Team management endpoint](https://cdn-images-1.medium.com/max/800/1*gaorKvd3BUxEl0nxbvCK9Q.png)
Internal Team management endpoint

After opening the endpoint (refer the Image above), the only thing running in my mind was “How about I check the directories.” Thus, I immediately utilized Dirsearch to brute force all the directories.

Here is the exciting output.

![I renamed dirsearch to \`dir\` because I am lazy :v](https://cdn-images-1.medium.com/max/800/1*qLcRlf4A_IQIWz7Qth1Xdw.png)
I renamed dirsearch to \`dir\` because I am lazy :v

**_Noticed? Anything?_**

It’s [https://37.--.--.--/register](http://s2.quickmeme.com/img/c5/c595586b491836bb2135fb603c2f4e5997ce0e2f8e41c30a81af650f568eaff8.jpg) :P

Upon opening the URL.

Yuss!!!! Registration page. 😮 anddd….

![](https://cdn-images-1.medium.com/max/800/1*SsXM8Vo5Wpip7hiaqVr-iw.png)

I tried to register with my details. And.. there was a configuration error. I was like…

I decided to register one more time with the same email and ended up with an error i.e.

**_“The email is already registered.”_**

okay, let’s go and log in.

So, I tried to log in with my registered credentials anddd…..

Successfully Logged in….

**_Admin management page._**

![All administrators name & email address was disclosed, I was even able to delete them.](https://cdn-images-1.medium.com/max/800/1*7tBKZpxAIOxG5wyUIDIGtg.png)
All administrators name & email address was disclosed, I was even able to delete them.

**Typical employee details pages**

Disclosed details include **Name, Email, Phone-No, Employee ID, Shifts, Reports, Salaries etc.**

![Typical Employee details (25k Records)](https://cdn-images-1.medium.com/max/800/1*AgTMv_sZ3X9ffgKF9pCP0Q.png)
Typical Employee details (25k Records)

**_Sorry,_** but I needed to hide some details due to confidentiality issues. Some other critical data was disclosing too but don’t have permission to write further.

After verifying the issue, I quickly submitted the detailed report to the program via HackerOne. They validated and fixed the problem within a few hours.

They permanently fixed the issue by removing the public registration page from the endpoint.

After reporting the issue, I applied _dirsearch_ on most of the critical endpoints belongs to them however no more endpoint was vulnerable to the same problem.

**Timeline**.

Report Submitted: **25–10–2017**

Report Triaged: **25–10–2017**

Initial **1300$** Awarded: **25–10–2017**

Report closed as Resolved: **25–10–2017**

Final **1200$** Awarded: **26–10–2017**

### Update

As many people messaging me and asking how I found this Asset/Internal team management endpoint. I am providing info about it here,

I found this endpoint using Github issues conversations.

### My recon process.

**Tools**

Sublister,knockpy,dnsresolver,dirsearch,bucket finder,massdns etc.

After reporting some low hanging issues, I go out and follow engineering/Security teams on Twitter and Github & look for anything interesting

I go through all the issues/Repositories companies engineering team created publicly on Github.

I read all blog posts by engineering and security team.

I check their DNS every month. Generally, companies stopped using a service and forgot to delete CNAMES pointing to service.

I use their services as the user and continue my recon processes,

I also use **Burp Suite pro history tool** to find exciting endpoints.

According to me, Recon is not a one time process it’s a continuous process.

**If you like my blog posts and my work, Please consider checking out my “Buy me a coffee” page**

[**Buy Me A Coffee - Best Way for Creators to Receive Tips**  
_Buy Me A Coffee help creators receive support from their audience in a friendly manner. Quickly accept donations and…_www.buymeacoffee.com](https://www.buymeacoffee.com/ZTExwKcRW "https://www.buymeacoffee.com/ZTExwKcRW")[](https://www.buymeacoffee.com/ZTExwKcRW)