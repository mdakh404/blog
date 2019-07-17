---
title: CTF Walkthrough — Hacken Cup 2018
description: >-
  Update-2 (07-Sept-2018): I just got the confirmation email from HackenProof
  that, my application is accepted for Hacken cup 2018 ❤
date: '2018-09-04T22:25:58.796Z'
categories: []
keywords: []
slug: /@ehsahil/ctf-walkthrough-hacken-cup-2018-1b48b0fd96c
---

**Update-2 (07-Sept-2018):** I just got the confirmation email from **HackenProof** that, my application is accepted for Hacken cup 2018 ❤

![❤ ❤ ❤](https://cdn-images-1.medium.com/max/800/1*VxXtgAmD94tWP1FL8gBqtQ.png)
❤ ❤ ❤

**Update-1**: I was planning to publish this walkthrough after the Hacken Cups results but since HackenProof already made the challenge public and I thought to publish it right away someone can use this walkthrough to solve the challenge.

Challenge is live for a few days I think, you can try to solve it.

Here is the updated post by HackenProof about the Hacken Cup.

[**A Change in Hacken Cup Application - HackenProof Blog**  
_Hacken Ecosystem We want to communicate a slight change in the application process for . Until this moment, in order to…_blog.hackenproof.com](https://blog.hackenproof.com/events/change-in-hacken-cup-application/ "https://blog.hackenproof.com/events/change-in-hacken-cup-application/")[](https://blog.hackenproof.com/events/change-in-hacken-cup-application/)

**Last year’s story**

HackIT Organised a 3rd security conference in Kharkiv, Ukraine last year, I was invited to the conference with all the expenses covered, they invited me via Twitter‘s DM and the invitation got into my Request folder somehow I haven’t seen it until the conference was finished.

![3rd Hackit Conference Invite.](https://cdn-images-1.medium.com/max/800/1*yyhL468BO5uaRAlFEHpbyg.png)
3rd Hackit Conference Invite.

my reaction seeing this message after the conference was finished.

SHIT !!!!!

I responded and told them, that message was in my twitter’s request folder, that’s why I have not responded.

![](https://cdn-images-1.medium.com/max/800/1*cUqS2jRx9_aNvzyYsYYc7w.png)

Now, let’s start the walkthrough — stay with me.

On **7-August-2018**, I got the following email from [HackenProof](https://hackenproof.com). Hackenproof is organizing onsite **Hacken Cup Bug Hunting Marathon** during HackIT 4.0 — The 4th Global CyberSecurity Forum in **Kyiv, Ukraine** from 8–11 October**.**

**Email from cup@hackenproof.com**

![](https://cdn-images-1.medium.com/max/800/1*KF3vcno72xVzBijrCymonQ.png)
![Screenshot of invitation email from HackenProof.](https://cdn-images-1.medium.com/max/800/1*FJFmMGUhwqjLlGzo2Xsg4w.png)
Screenshot of invitation email from HackenProof.

I received the email on my mobile, I clicked on **Apply** but the button didn’t work, I quickly logged into my Gmail via mac and clicked on **Apply** again. Still not working.

huhhh!!!??

Then I saw a message at the bottom of the email.

**P.S. Follow the white rabbit**

Hmm, Something is interesting.

hmm…something is interesting.

After trying few things, I used “**Show Original**” Option from Gmail and searched for “Apply” keyword.

![Found an external IP address.](https://cdn-images-1.medium.com/max/800/1*jdPHR0qJpwohJ9gNLDgUtA.png)
Found an external IP address.

Got an external IP address. :

[http://159.65.204.68](http://159.65.204.68)

opened it in Google Chrome, the following page appeared

![You shall????](https://cdn-images-1.medium.com/max/800/1*VYl16aYf6gQazVCSJXtgaw.png)
You shall????

You shall what?

Checked the source code: got two images.

http://159.65.204.68/images/404–2–41.png

[http://159.65.204.68/images/W9Yjy17.jpg](http://159.65.204.68/images/W9Yjy17.jpg)

and also, a sweet message

**It would be too easy :)**

![It really was too easy.](https://cdn-images-1.medium.com/max/800/1*aMbm6USXOvWuo0_NYQ1EZQ.png)
It really was too easy.![You shall not hack???](https://cdn-images-1.medium.com/max/800/1*aAIqA8k9s-X3LiQw5WfdRw.png)
You shall not hack???

You shall not \*\*\*\*? You shall not hack?

I searched it on **Google** and found out that its a quote from the movie “T**he Lord of the rings.”**

**YOU SHALL NOT PASS!!!**

You Shall Not Pass!!!!!

Sure, I am not passing.

I started my recon process for the endpoint.

1.  Nmap — **159.65.204.68**

nmap -sV 159.65.204.68

![Lots of ports are open](https://cdn-images-1.medium.com/max/800/1*ds_gA3Mx5-5Xf5AlNu18GA.png)
Lots of ports are open

Got many open ports and I left them to see later and I tried to see if I can find something interesting via dirsearch.

2\. [Dirsearch](https://github.com/maurosoria/dirsearch) — 159.65.204.68

python3 dirsearch.py -u [http://159.65.204.68](http://159.65.204.68) -e \*

![](https://cdn-images-1.medium.com/max/800/1*Hasb9Iim-ctUpOlV1tLrDA.png)

After running Dirsearch, I found a publicly available **.git** directory and used **Dumper** tool from [**Gittools**](https://github.com/internetwache/GitTools) to download the available git directory locally.

I cloned the .git files using the following command.

bash gitdumper.sh [http://159.65.204.68/.git/](http://159.65.204.68/.git/) ehsahil

Gitdumper cloned the publicly available git files into a folder ‘**ehsahil**’

![](https://cdn-images-1.medium.com/max/800/1*Lk4TEiioP4aT5vPhngPp_Q.png)

After downloading the git directory locally. I manually go through all the files and directories available publicly.

![](https://cdn-images-1.medium.com/max/800/1*A4BaQnAVuzr1Fa_-vHMoQw.png)

After getting commit information and other I got inside the objects folders, which contains large numbers of objects.

I found objects folder interesting and decided to look into all of them.

![](https://cdn-images-1.medium.com/max/800/1*kqknroiKbdBBdAClE-WfRw.png)

It’s time to find the object Ids. For that, I used **find** command

find -type f

I got the following result with all the object-ids.

![](https://cdn-images-1.medium.com/max/800/1*BovFu-OxomdOI8HqsNeI1g.png)

I have to remove all the dots(.) and forward slashes from the above result using **sed**.

```
sed -e 's/\.//g'
```

Saved all object id in an objectids.txt file.

Now, I got all the Object IDs, its time to cat every file to see the contents.

git cat-file -p <object\_id>

But manually viewing the contents of the all the objects was time-consuming.

that’s why I tried to automate the process, I created a small ruby script to fetch contents from all Objectid’s.

Here is the sweet and small ruby script. — git.rb

require 'socket'  
require 'colorize'

begin    
  file = File.open(ARGV\[0\], "r")  
rescue  
  puts "Usage: ruby git.rb objectsid"   
  exit  
end   
file.each\_line do |objects|  
puts    
puts "Content of ObjectID --> #{objects}"   
puts "+--------------------------------------------------------+"                          system("git cat-file -p #{objects}")   
puts "Moving to next ObjectID"   
puts  puts "+--------------------------------------------------+"  end

After running the ruby script, I found the index.php source code in **37** Object Folder.

I tried to concatenate the Objectid manually,

![My credentials are my credentials none of your credentials !!!](https://cdn-images-1.medium.com/max/800/1*CoNK1GJUxjAldyaYEzF6Tg.png)
My credentials are my credentials none of your credentials !!!Pheww!!!

Credentials for admin panel.

$username = ‘[admin@cup.hackenproof.com](mailto:admin@cup.hackenproof.com)’;  
$password = ‘Qd79E0FL&R’;

Then, I quickly browse to [http://159.65.204.68/admin](http://159.65.204.68/admin) to see the credentials whether the credentials will work or not.

[http://159.65.204.68/admin](http://159.65.204.68/admin)

![ADMIN login page.](https://cdn-images-1.medium.com/max/800/1*RD1EjmerzjON65TOwls23w.png)
ADMIN login page.

Credentials have WORKED!!! Yus!!!

After login, application redirected me to the following page with a file uploading functionality.

http://159.65.204.68/admin/index.php

![Admin File uploading endpoint.](https://cdn-images-1.medium.com/max/800/1*jvAkm0ly38FDs0NuVMdP7A.png)
Admin File uploading endpoint.ALRIGHT!
![Index.php Source Code](https://cdn-images-1.medium.com/max/800/1*14reeCnGumQG9t2Lu3-cUQ.png)
Index.php Source Code

Reviewing the index.php file from the objects folder.

1.  Index.php is only checking for **mimetype** (**image/jpeg, image/gif, image/png**) to validate the uploaded image is indeed an image or not.

2\. Application is uploading the user file on the

**/var/www/html/admin/uploads** that means

http://159.65.204.68/admin/uploads/<Uploaded-file-name>

3\. **(preg\_match(‘/.php$/’,$file)) — **Here the endpoint is only checking for **php** extension in the filename.

there are many bypasses for this type lousy PHP file validation protection.

One of them is by using **php5** as  an  extension instead of **php** to bypass the protection.

![](https://cdn-images-1.medium.com/max/600/1*w_nbJktLF28NszsjVWJvfg.png)
![file with .php extension is not uploading as expected.](https://cdn-images-1.medium.com/max/600/1*YOQT7dzVzcWH7dv4CIPK5A.png)
file with .php extension is not uploading as expected.

![](https://cdn-images-1.medium.com/max/600/1*BX378IxAp7ezUWflg47hKg.png)
![Uploaded php file with .php5 extension and file was successfully uploaded.](https://cdn-images-1.medium.com/max/600/1*FLPU1_ETOfkK5WtHtSbzXQ.png)
Uploaded php file with .php5 extension and file was successfully uploaded.

Uploaded PHP file with “**1337.jpg.php5**” extension and content-type: **image/jpeg**

I used **p0wny-shell** — [https://github.com/flozz/p0wny-shell](https://github.com/flozz/p0wny-shell)

![](https://cdn-images-1.medium.com/max/800/1*odd9chs2bcNn3V84UPNEpA.png)

p0wny shell is successfully uploaded and executed.

After that, I browsed through the internal file system to find the interesting files and hints for the next level.

![](https://cdn-images-1.medium.com/max/800/1*K6FZ5rwQ2Yy0UypB77Cyaw.png)

😮 found “**congrats.html**” in **/super\_secret\_cup** directory.

I didn’t see that coming.

let’s see the content of the congrats.html

**FINALLY**!! the Private Google docs form link to apply for HackenProof CUP 2018.

![cat congrats.html](https://cdn-images-1.medium.com/max/800/1*KpvMPcTMOe_fMXijZSVtpA.png)
cat congrats.html

Let’s Open the “congrats.html” in the browser.

![HackenProof you guys are Awesome too.](https://cdn-images-1.medium.com/max/800/1*UmGQ7gp4uBuwJO1q__h0mw.png)
HackenProof you guys are Awesome too.

AND…. Google form for Hacken Cup. 😍😍

![](https://cdn-images-1.medium.com/max/800/1*7DnRCjr0E6muVNzdAPhsSw.png)

Thanks, **HackenProof and Hackit Team** for allowing me to participant in the **HackenProof** Cup 2018 Challenge.

Publishing on 05-Sept-2018 at 3:55 AM Indian Standard Time (IST),

**If you like my blog posts and my work, Please consider checking out my “Buy me a coffee” page**

[**Buy Me A Coffee - Best Way for Creators to Receive Tips**  
_Buy Me A Coffee help creators receive support from their audience in a friendly manner. Quickly accept donations and…_www.buymeacoffee.com](https://www.buymeacoffee.com/ehsahil "https://www.buymeacoffee.com/ehsahil")[](https://www.buymeacoffee.com/ehsahil)

until next time.