---
layout: post
title: Recon — my way.
---

A detailed blog post on my reconnaissance processes for web applications security testing. I always wanted to write about this subject being asked by many friends, community members, etc. but I hooked wasting a lot of hours on a Meme Channel & The Big Bang Theory TV Series.

#### UPDATE: I created a GitHub repository with tools from this post and personal installation guide.

* [**ehsahil/recon-my-way**  ](https://github.com/ehsahil/recon-my-way "https://github.com/ehsahil/recon-my-way")[](https://github.com/ehsahil/recon-my-way)


Recently, some new members of the InfoSec community asked me to share my recon process. Hence, I decided to begin writing this blog and tried to include such tools and services which helps me a lot while testing and will help the readers too, for sure.

#### Summary

1.  **Introduction**
2.  **A tool I modified.**
3.  **Visual recon**
4.  **More Assets — More findings — More win.**
5.  **Data Storage Buckets.**
6.  **Github for Recon.**
7.  **Read Every JS**
8.  **Archive**
9.  **Continuous Recon**
10.  **Extra points for recon.**

### 1\. Introduction

Whenever I get an invitation for a new program or I want to test a target, I start my recon process by using the [**Knockpy**](https://github.com/guelfoweb/knock).

Why I use knockpy Initially? It provides me with a quick overlook of the subdomains with a response code.

Once, I found a subdomain takeover bug within 2 mins.

I ran knockpy on an old program’s in-scope asset with almost 150 bugs resolved on [HackerOne](https://medium.com/u/6f816e37be2c). Quickly saw 404 page pointed to AWS S3 bucket and bucket were available to create. Hence, with no delay, I created the new AWS S3 bucket and uploaded a text file with the encoded filename and reported the bug and guess what? I got the bounty that too within 15 mins.

Lesson: knockpy = quick win

![see 404 error in above screenshot == Quick win.](https://cdn-images-1.medium.com/max/800/1*9rx6jBUwgCBr77YgZHsYCQ.png)


### 2\. A Tool I Modified.

I use a customized tool for subdomain reconnaissance.

I used a resolver tool by [Malvinsh](https://github.com/melvinsh/subresolve) and customized it.

* [**melvinsh/subresolve**  ](https://github.com/melvinsh/subresolve "https://github.com/melvinsh/subresolve")[](https://github.com/melvinsh/subresolve)

Malvinsh resolver tool runs as.

![Malvinsh Tools Original output.](https://cdn-images-1.medium.com/max/800/1*GasU0Zkt5dExaYGkgoTw3Q.png)
Malvinsh Tools Original output.

[Malvinsh](https://github.com/melvinsh/subresolve) tool is doing two simple processes.

*   Getting the IP address of the domain/subdomain from the wordlist using **HOST.**
*   Performing the Nmap scan.

Using its logic I created two scripts.

*   **subdomain.rb** [**gist**](https://gist.github.com/ehsahil/0b618104319a97b21bea88fbb5ea49c2)**.**
*   **recon.rb** [**gist**](https://gist.github.com/ehsahil/f0f6e731a22a111399aa8503e34b6919)**.**

**Caution:** Do not use these scripts on programs where automatic testing is forbidden and also on the targets on which you are not allowed to.

#### Subdomain.rb

**Subdomain.rb** is a lightweight script to automate tools for subdomain finding and it’s damn flexible — more tools can be added easily.

Subfinder and sublist3r results sometime overlap. I tried to run both tools separately on a particular asset and got some distinct results — that’s why I kept both tools in this script.

The script is using the following tools to get the subdomains data.

*   [**Ice3man543/subfinder**  ](https://github.com/Ice3man543/subfinder "https://github.com/Ice3man543/subfinder")[](https://github.com/Ice3man543/subfinder)

*   [**christophetd/censys-subdomain-finder** ](https://github.com/christophetd/censys-subdomain-finder "https://github.com/christophetd/censys-subdomain-finder")[](https://github.com/christophetd/censys-subdomain-finder)

*   [**guelfoweb/knock** ](https://github.com/guelfoweb/knock "https://github.com/guelfoweb/knock")[](https://github.com/guelfoweb/knock)

*   [**aboul3la/Sublist3r** ](https://github.com/aboul3la/Sublist3r "https://github.com/aboul3la/Sublist3r")[](https://github.com/aboul3la/Sublist3r)



* [**michenriksen/aquatone** ](https://github.com/michenriksen/aquatone "https://github.com/michenriksen/aquatone")[](https://github.com/michenriksen/aquatone)



**subdomain.rb** [**gist**](https://gist.github.com/ehsahil/0b618104319a97b21bea88fbb5ea49c2)**.**

> **Usage: ruby subdomain.rb domain.com**

![Subdomain.rb demo run.](https://cdn-images-1.medium.com/max/800/1*Y2PA3Sxfce0beCT4N1RQjw.gif)

I, usually, create a file and add all subdomains from the above outputs. Then, I use the **sort** command to delete all duplicate/overlapped subdomains from the file.

> **sort wordlist | uniq**

I pass the final unique subdomains file to the recon.rb

#### Resolve.rb

Recon.rb is another lightweight script and it is also flexible hence, more tools can be added easily.Tools included in recon.rb

*   **Host** : Resolve the subdomain.
*   **Nmap** : Perform Port scan on subdomain

*   [**Nmap: the Network Mapper — Free Security Scanner** ](https://nmap.org/ "https://nmap.org/")[](https://nmap.org/)

*   [**AWS Command Line Interface** ](https://aws.amazon.com/cli "https://aws.amazon.com/cli")[](https://aws.amazon.com/cli)

*   [**maurosoria/dirsearch**  ](https://github.com/maurosoria/dirsearch "https://github.com/maurosoria/dirsearch")[](https://github.com/maurosoria/dirsearch)


**recon.rb** [**gist**](https://gist.github.com/ehsahil/f0f6e731a22a111399aa8503e34b6919)**.**

> **Usage: ruby recon.rb wordlist**

![Recon.rb demo run.](https://cdn-images-1.medium.com/max/800/1*SnV-UF4dxE1-iJoU6jcnlg.gif)

A tool with Above functionality in the organized fashion.

* [**nahamsec/lazyrecon** ](https://github.com/nahamsec/lazyrecon "https://github.com/nahamsec/lazyrecon")[](https://github.com/nahamsec/lazyrecon)

**Interesting blog posts**

* [**\[BugBounty\] Decoding a $😱,000.00 htpasswd bounty** ](https://blog.it-securityguard.com/bugbounty-decoding-a-%F0%9F%98%B1-00000-htpasswd-bounty/ "https://blog.it-securityguard.com/bugbounty-decoding-a-%F0%9F%98%B1-00000-htpasswd-bounty/")[](https://blog.it-securityguard.com/bugbounty-decoding-a-%F0%9F%98%B1-00000-htpasswd-bounty/)

* [**Scanning the Alexa Top 1M for .DS\_Store files** ](https://en.internetwache.org/scanning-the-alexa-top-1m-for-ds-store-files-12-03-2018/ "https://en.internetwache.org/scanning-the-alexa-top-1m-for-ds-store-files-12-03-2018/")[](https://en.internetwache.org/scanning-the-alexa-top-1m-for-ds-store-files-12-03-2018/)

### 3\. Visual Recon

I use the previously generated wordlist from subdomian.rb for visual recon.

I generally use the following two tools.

*   [**maaaaz/webscreenshot** ](https://github.com/maaaaz/webscreenshot "https://github.com/maaaaz/webscreenshot")[](https://github.com/maaaaz/webscreenshot)

![](https://cdn-images-1.medium.com/max/800/1*k_HXhIWo8TvbADiM_Skw-g.png)

*   [**mdhama/lazyshot** ](https://github.com/mdhama/lazyshot "https://github.com/mdhama/lazyshot")[](https://github.com/mdhama/lazyshot)

![](https://cdn-images-1.medium.com/max/800/1*XnDnEykchL_PlM0Lt4146g.png)

**Interesting blog posts**

* [**\[Tools\] Visual Recon — A beginners guide** ](https://blog.it-securityguard.com/visual-recon-a-beginners-guide/ "https://blog.it-securityguard.com/visual-recon-a-beginners-guide/")[](https://blog.it-securityguard.com/visual-recon-a-beginners-guide/)

### 4\. More Assets — More findings — More win.

I go for this section after reporting 2–3 issues in a particular program and wait for the response, if I find program interesting then I try to collect as much information as I can about the target using the following services.


* [**yamakira/censys-enumeration** ](https://github.com/yamakira/censys-enumeration "https://github.com/yamakira/censys-enumeration")[](https://github.com/yamakira/censys-enumeration)



*  [**Shodan** ](https://www.shodan.io/ "https://www.shodan.io/")[](https://www.shodan.io/)

```
Shodan Basic Commands. 

443.https.tls.certificate.parsed.extensions.subject_alt_name.dns_names:domain.com

“hackme.tld” + internal 

“hackme.tld” + sandbox

“hackme.tld” + Staging

“hackme.tld” + Development/Dev

“hackme.tld” +  production/prod

 hackme inc
 
 Credit: @nahamsec
 
 Interesting posts: 
 https://0xpatrik.com/censys-guide/
```

*   [**ViewDNS.info — Your one source for DNS related tools!**  ](http://viewdns.info/ "http://viewdns.info/")[](http://viewdns.info/)


Get the whois information of target using whois command or use an online tool.

> **whois domain.com**

If the company is not using Domain Privacy Service,

you will find the host-masters email address then use that email to find other domains registered on same email address using Reverse Whois Lookup. Targets Registered legal name also can be used.

![Result for hackeone inc query](https://cdn-images-1.medium.com/max/800/1*Z5xCr_GbcYYx2cNYfzSEKA.png)


*   [**IP range Crawl**](https://bgp.he.net/)

![IP range for hackerone.com](https://cdn-images-1.medium.com/max/800/1*TkfmlFDVAFbL4Mn9JFQEbg.png)


*   [**infosec-au/altdns** ](https://github.com/infosec-au/altdns "https://github.com/infosec-au/altdns")[](https://github.com/infosec-au/altdns)


*   **Nmap Subdomain finding.**

```
#Finding subdomains via Nmap. 

nmap --script dns-brute --script-args dns-brute.domain=domain.com,dns-brute.threads=6,dns-brute.hostlist=./sub1000.lst

nmap --script dns-brute --script-args dns-brute.domain=domain.com,dns-brute.threads=6,dns-brute.hostlist=./sub10000.lst

nmap --script dns-brute --script-args dns-brute.domain=domain.com,dns-brute.threads=6,dns-brute.hostlist=./sub100000.lst

nmap --script dns-brute --script-args dns-brute.domain=domain.com,dns-brute.threads=6,dns-brute.hostlist=./sub1000000.lst


#Wordlist : 

1. sub1000.lst - https://drive.google.com/open?id=0B0h-Dh0Oss1zOGFqVVl1bTVpdWc
2. sub10000.lst - https://drive.google.com/open?id=0B0h-Dh0Oss1zTTdmQnZsQ0JCYzA
3. sub100000.lst - https://drive.google.com/open?id=0B0h-Dh0Oss1zdDBFT1dCc08ya0U
4. sub1000000.lst - https://drive.google.com/open?id=0B0h-Dh0Oss1zODNfSG1sbVJ1WE0

In case above links are not available : https://github.com/ehsahil/wordlists-for-nmap

#Taken from http://blog.x1622.com/2016/11/subdomain-discovery-with-nmap-and.html

```


* [**yamakira/domains-from-csp**  ](https://github.com/yamakira/domains-from-csp "https://github.com/yamakira/domains-from-csp")[](https://github.com/yamakira/domains-from-csp)

* [**Analyse your HTTP response headers** ](https://securityheaders.com/ "https://securityheaders.com/")[](https://securityheaders.com/)


*   [**eldraco/domain\_analyzer** ](https://github.com/eldraco/domain_analyzer "https://github.com/eldraco/domain_analyzer")[](https://github.com/eldraco/domain_analyzer)



*   [**jpf/domain-profiler**  ](https://github.com/jpf/domain-profiler "https://github.com/jpf/domain-profiler")[](https://github.com/jpf/domain-profiler)


*   [**codingo/VHostScan** ](https://github.com/codingo/VHostScan "https://github.com/codingo/VHostScan")[](https://github.com/codingo/VHostScan)


*  [**Visual Site Mapper — Create a visual map of your site** ](http://www.visualsitemapper.com/ "http://www.visualsitemapper.com/")[](http://www.visualsitemapper.com/)



* [**Google Transparency Report** ](https://transparencyreport.google.com/https/certificates "https://transparencyreport.google.com/https/certificates")[](https://transparencyreport.google.com/https/certificates)

*   [**https://certspotter.com/api/v0/certs?domain=hackerone.com**](https://certspotter.com/api/v0/certs?domain=domain.com)


*   [**CertDB — SSL certificates search engine** ](https://certdb.com/ "https://certdb.com/")[](https://certdb.com/)



*   [**Crt.sh**](https://crt.sh/?q=%25domain.com)[](https://crt.sh/?q=%25domain.com)



*   [**Certificate Transparency Monitoring — Facebook for Developers** ](https://developers.facebook.com/tools/ct "https://developers.facebook.com/tools/ct")[](https://developers.facebook.com/tools/ct)



![Facebook Crt transparency monitoring subscriptions.](https://cdn-images-1.medium.com/max/800/1*KogNCTgMlSQmARkFplHBwA.png)

    Facebook Crt transparency monitoring subscriptions.

![Typical notification from Facebook when new asset on the same crt is available.](https://cdn-images-1.medium.com/max/800/1*dcLY8QxDdE88CoUlF1tHSg.png)
Typical notification from Facebook when new asset on the same crt is available.

**Interesting blog posts & tools taken from**

* [**Asset Discovery: Doing Reconnaissance the Hard Way**  ](https://0xpatrik.com/asset-discovery/ "https://0xpatrik.com/asset-discovery/")[](https://0xpatrik.com/asset-discovery/)

* [**Subdomain Takeover: Thoughts on Risks**  ](https://0xpatrik.com/subdomain-takeover/ "https://0xpatrik.com/subdomain-takeover/")[](https://0xpatrik.com/subdomain-takeover/)

* [**Subdomain Takeover: Proof Creation for Bug Bounties** ](https://0xpatrik.com/takeover-proofs/ "https://0xpatrik.com/takeover-proofs/")[](https://0xpatrik.com/takeover-proofs/)

* [**Project Sonar: An Underrated Source of Internet-wide Data**  ](https://0xpatrik.com/project-sonar-guide/ "https://0xpatrik.com/project-sonar-guide/")[](https://0xpatrik.com/project-sonar-guide/)

* [**EdOverflow/can-i-take-over-xyz**  ](https://github.com/EdOverflow/can-i-take-over-xyz "https://github.com/EdOverflow/can-i-take-over-xyz")[](https://github.com/EdOverflow/can-i-take-over-xyz)

### 5\. Data Storage Buckets.

Common Places to find Data Storage buckets.

*   Github
*   Javascript files
*   CSP Headers
*   Archive crawl
*   Pastebin

Tip: If a bucket is returning access denied. Try to search it on Google. There are good chances that the team has recently changed the permissions of the bucket and specific files have been indexed by Google (which are available with read permission).

If the application has file uploading functionality, then try to capture the file uploading request and see where the file is being uploaded. Sometimes you will find AWS or other data storage buckets, which cannot be detected by any other method.

If you find the bucket like **upload-user-content-target-prod **— try to change the prod to dev, staging, sandbox, etc.

*   [**AWS CLI**](https://aws.amazon.com/cli/) — AWS CLI is useful for verifying or testing the permissions of the AWS S3 buckets, Creating Buckets and Read other buckets data. AWS Account needed to use CLI.

*   [**Bucket Finder — DigiNinja** ](https://digi.ninja/projects/bucket_finder.php "https://digi.ninja/projects/bucket_finder.php")[](https://digi.ninja/projects/bucket_finder.php) — **Great Tool for finding buckets using subdomains wordlist, can be integrated into recon.rb script but I don’t always use it.


*   [**nahamsec/lazys3**  ](https://github.com/nahamsec/lazys3 "https://github.com/nahamsec/lazys3")[](https://github.com/nahamsec/lazys3) — LazyS3 is an another tool which I use almost frequently to find the staging, sandboxed, dev and production buckets.



*   [**gwen001/s3-buckets-finder**  ](https://github.com/gwen001/s3-buckets-finder "https://github.com/gwen001/s3-buckets-finder")[](https://github.com/gwen001/s3-buckets-finder)— Another good tool for AWS S3 buckets.


**Interesting blog post**

* [**A deep dive into AWS S3 access controls — taking full control over your assets** ](https://labs.detectify.com/2017/07/13/a-deep-dive-into-aws-s3-access-controls-taking-full-control-over-your-assets/ "https://labs.detectify.com/2017/07/13/a-deep-dive-into-aws-s3-access-controls-taking-full-control-over-your-assets/")[](https://labs.detectify.com/2017/07/13/a-deep-dive-into-aws-s3-access-controls-taking-full-control-over-your-assets/)

### 6\. Github For Recon.

Github is extremely helpful in finding Sensitive information regarding the targets. Access-keys, password, open endings, s3 buckets, backup files, etc. can be found on public GitHub repositories.

**Interesting blog post**

* [**GitHub for Bug Bounty Hunters**  ](https://edoverflow.com//2017/github-for-bugbountyhunters "https://edoverflow.com//2017/github-for-bugbountyhunters")[](https://edoverflow.com//2017/github-for-bugbountyhunters)

### 7\. Read every JS.

Sometimes, Javascript files contain sensitive information including various secrets or hardcoded tokens. It’s always worth to examine JS files manually.

I have found the following things in Javascript.

*   AWS or Other services Access keys
*   AWS S3 buckets or other data storage buckets with read/write permissions.
*   Open backup sql database endpoints
*   Open endpoints of internal services.

The more Javascript files you read, the more chances will be of win.

**Tools**

I generally like to read the javascript code manually with the help of JSBeautifier.

* [**Online JavaScript beautifier**  ](http://jsbeautifier.org/ "http://jsbeautifier.org/")[](http://jsbeautifier.org/)

* [**GerbenJavado/LinkFinder**  ](https://github.com/GerbenJavado/LinkFinder "https://github.com/GerbenJavado/LinkFinder")[](https://github.com/GerbenJavado/LinkFinder)

* [**nahamsec/JSParser**  ](https://github.com/nahamsec/JSParser "https://github.com/nahamsec/JSParser")[](https://github.com/nahamsec/JSParser)


**Interesting blog post**

* [**Bug Bounty — Tips / Tricks / JS (JavaScript Files)**  ](https://medium.com/bugbountywriteup/bug-bounty-tips-tricks-js-javascript-files-bdde412ea49d "https://medium.com/bugbountywriteup/bug-bounty-tips-tricks-js-javascript-files-bdde412ea49d")[](https://medium.com/bugbountywriteup/bug-bounty-tips-tricks-js-javascript-files-bdde412ea49d)

### 8\. [Archive](http://archive.org/web/)

Searching for the targets webpages in [waybackmachine](http://archive.org/web/), the following things can be found.

*   Old and abandoned JS files.
*   Old API endpoints.
*   Abandoned CDN’s Endpoints.
*   Abandoned Subdomains.
*   Dev & staging endpoint with juicy info in source code comments.

If you are getting 403 on a page, you can also search that 403 pages of targets in way back machine sometimes, you will find them open with helpful information.

**Tool**: [Waybackurl](https://gist.github.com/mhmdiaa/adf6bff70142e5091792841d4b372050)

### 9\. Continuous Recon.

*   The most essential thing in continuous recon is handling of the recon data for the future uses, for this, [**SecurityEscape**](https://securityescape.com) created a tool known as **Swiftness.** I use Swiftness to hold all of my recon data for every target.

![Swiftness- My personal websec checklist.](https://cdn-images-1.medium.com/max/800/1*BoAy1Lr5DZDWMABMuyBlGw.png)
Swiftness- My personal websec checklist.

*   I use the reminder to revisiting the targets and perform recon regularly. (Every month)

### 10\. Extra points for recon.

**Note**: I have provided some data in gist because I regularly update them and those updates will be automatically available here.

```
Tips from @jobertabma, co-founder of HackerOne -- https://twitter.com/jobertabma/status/998769037445230592

0x00: I visit the product and marketing pages and read up what the products do. I identify how the product it exposed to the end user. This will give me an idea what the initial attack surface looks like, what data they're protecting, how users interact with each other, and what the learning curve looks like. I sign up for any number of accounts that is required to test the features. This will give me insight into the individual features. I do some light fingerprinting of the frameworks they use.I've even talked to engineers, product managers, and executives before even looking at something.

0x01: I prioritize based on features and then weakness type. I generally set a goal for myself to go after particular information, e.g. for an email provider I might ask myself: "I want to get access to someone's emails." Because I know what their features do, I can make an educated guess which features process emails. This is where I will look for vulnerabilities first and prioritize weaknesses that could give access (e.g. IDOR) before others (e.g. XSS). Some features contain more vulnerabilities than others.
Rule of thumb: the more complex the feature is, the more likely it is it contains vulnerabilities. I never check for two weakness types at the same time. I usually time box looking at a feature, often to avoid going down a rabbit hole and wasting time.
It's often better to pause, take notes on the behavior you observed, and move on. I've had multiple (shower) "aha" moments where I connected the dots later. I don't always find something. That's OK. Work through the system's features until you run out of endpoints.

0x02: Only then do I focus on expanding my attack surface. I use http://archive.org , their (minified) JavaScript files, documentation, schemas, and best guesses to find these. Personally, I hardly ever brute force files and directories. In this process,I place myself in the head of an engineer of the company and ask myself: "If I were to build feature x, what would I have to do?" This question helps me identify where technical debt is and how I can automate the detection of new features.
I'm not a mayfly: I pick a target and often stick with it for months instead of switching targets frequently. I actually think I'd do fine as a junior engineer at most of my targets. It allows me to build a relationship with the team.

0x03: I'm familiar with a wide range of vulnerability types. I've only gotten there by creating structure in my work and setting goals. I never start from a vulnerability type, always from an indication something may be vulnerable or a feature.
If I come across technology I haven't used yet, I often take a step back and use it outside of the application's context. This will increase my frame of reference and understand how the technology is used within the system.
I use bug bounties as a way to expand my knowledge, not to treat it as a race. It has helped me being an engineer first. Throughout the process I make extensive notes (with http://recon.sh , see my GitHub).

0x04: I write simple scripts and use available tools to help me in my process of expanding my attack surface. I've written tools who'd email me a weekly diff of endpoints found in a JavaScript file or code linters to point out dangerous functions or complex code patterns.
I use a combination of @culturedcode and http://recon.sh ! I haven't used mind maps because of the lack of similarity between features across different assets. There's some process to be put in place there and it might help, I've just never done it myself.

Full disclosure: I rarely use them. The stuff that people find during recon, I find when I have a reason to look for it, so you could say I don’t do recon like the majority of the community does their recon. When I do, I’ve used https://gist.github.com/jhaddix .

Of course! Here are some Quora answers that I've written in the past that might help answer your question: https://www.quora.com/How-does-one-become-a-bug-bounty-hunter/answer/Jobert-Abma …, https://www.quora.com/How-much-time-did-you-take-from-completely-beginning-hacking-to-your-first-success-or-bug-bounty/answer/Jobert-Abma …, https://www.quora.com/How-do-bug-bounty-hunters-find-bugs/answer/Jobert-Abma …, https://www.quora.com/What-things-should-I-learn-to-become-a-bug-bounty-hunter-Should-I-start-by-learning-programming-languages-I-am-17-years-old/answer/Jobert-Abma …, and https://www.quora.com/What-can-I-do-as-a-high-school-student-to-get-into-bug-bounty-hunting/answer/Jobert-Abma …. Let me know if that helped!

Personal: 

1. Follow security and engineering team members on twitter. 
2. Read all engineering/dev blog posts available. 
3. Use the Company services as a normal user if you can. 
4. Reading commits and public issues conversations on Github.
5. Reading robots.txt files. 
6. Be familiar with the companies dev stacks and use them if you can.
7. Watch target companies videos on youtube or on other platforms about new products, demo, conference etc. 
8. Search for the information about the targets on Pastebin and trello etc.
9. Searching swf, txt, xml etc files using Search Engines dork.
10. Initially, I report only 2-3 issues with little recon. 
11. Follow other security researchers on social networking sites. 
```


Best of luck for all of your future infosec things.

If you have questions and anything about the post you want to ask me, Please contact me via twitter/fb. I’ll have my DM open.

Feedbacks and edits are welcome

[**Buy Me A Coffee - Best Way for Creators to Receive Tips** ](https://www.buymeacoffee.com/ehsahil "https://www.buymeacoffee.com/ehsahil")[](https://www.buymeacoffee.com/ehsahil)
