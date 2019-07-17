---
layout: post
title: Recon — my way.
---

A detailed blog post on my reconnaissance processes for web applications security testing. I always wanted to write about this subject being asked by many friends, community members, etc. but I hooked wasting a lot of hours on a Meme Channel & The Big Bang Theory TV Series.

#### UPDATE: I created a GitHub repository with tools from this post and personal installation guide.

[**ehsahil/recon-my-way**  ](https://github.com/ehsahil/recon-my-way "https://github.com/ehsahil/recon-my-way")[](https://github.com/ehsahil/recon-my-way)


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

[**melvinsh/subresolve**  ](https://github.com/melvinsh/subresolve "https://github.com/melvinsh/subresolve")[](https://github.com/melvinsh/subresolve)

Malvinsh resolver tool runs as.

![Malvinsh Tools Original output.](https://cdn-images-1.medium.com/max/800/1*GasU0Zkt5dExaYGkgoTw3Q.png)
Malvinsh Tools Original output.

[Malvinsh](https://github.com/melvinsh/subresolve) tool is doing two simple processes.

*   Getting the IP address of the domain/subdomain from the wordlist using **HOST.**
*   Performing the Nmap scan.

Using its logic I created two scripts.

*   **Subdomain.rb**
*   **Recon.rb**

**Caution:** Do not use these scripts on programs where automatic testing is forbidden and also on the targets on which you are not allowed to.

#### Subdomain.rb

**Subdomain.rb** is a lightweight script to automate tools for subdomain finding and it’s damn flexible — more tools can be added easily.

Subfinder and sublist3r results sometime overlap. I tried to run both tools separately on a particular asset and got some distinct results — that’s why I kept both tools in this script.

The script is using the following tools to get the subdomains data.

*   [Subfinder](https://github.com/Ice3man543/subfinder)

[**Ice3man543/subfinder**  ](https://github.com/Ice3man543/subfinder "https://github.com/Ice3man543/subfinder")[](https://github.com/Ice3man543/subfinder)

*   [Censys subdomain finder.](https://github.com/christophetd/censys-subdomain-finder)

[**christophetd/censys-subdomain-finder** ](https://github.com/christophetd/censys-subdomain-finder "https://github.com/christophetd/censys-subdomain-finder")[](https://github.com/christophetd/censys-subdomain-finder)

*   [Knockpy](https://github.com/guelfoweb/knock)

[**guelfoweb/knock**  
_knock — Knock Subdomain Scan_github.com](https://github.com/guelfoweb/knock "https://github.com/guelfoweb/knock")[](https://github.com/guelfoweb/knock)

*   [Sublist3r](https://github.com/aboul3la/Sublist3r)

[**aboul3la/Sublist3r**  
_Sublist3r — Fast subdomains enumeration tool for penetration testers_github.com](https://github.com/aboul3la/Sublist3r "https://github.com/aboul3la/Sublist3r")[](https://github.com/aboul3la/Sublist3r)

*   [Aquatone](https://github.com/michenriksen/aquatone)

[**michenriksen/aquatone**  
_aquatone — A Tool for Domain Flyovers_github.com](https://github.com/michenriksen/aquatone "https://github.com/michenriksen/aquatone")[](https://github.com/michenriksen/aquatone)

**subdomain.rb** [**gist**](https://gist.github.com/ehsahil/0b618104319a97b21bea88fbb5ea49c2)**.**

> **Usage: ruby subdomain.rb domain.com**

![Subdomain.rb demo run.](https://cdn-images-1.medium.com/max/800/1*Y2PA3Sxfce0beCT4N1RQjw.gif)
Subdomain.rb demo run.

I, usually, create a file and add all subdomains from the above outputs. Then, I use the **sort** command to delete all duplicate/overlapped subdomains from the file.

> **sort wordlist | uniq**

I pass the final unique subdomains file to the recon.rb

#### Resolve.rb

Recon.rb is another lightweight script and it is also flexible hence, more tools can be added easily.Tools included in recon.rb

*   **Host** : Resolve the subdomain.
*   **Nmap** : Perform Port scan on subdomain

[**Nmap: the Network Mapper — Free Security Scanner**  
_Nmap Free Security Scanner, Port Scanner, & Network Exploration Tool. Download open source software for Linux, Windows…_nmap.org](https://nmap.org/ "https://nmap.org/")[](https://nmap.org/)

*   **AWS CLI — **In the script AWS, CLI used test subdomains are connected to AWS bucket or not also checks for list permission. (Can be customized to test for write permission files.)

[**AWS Command Line Interface**  
_The AWS Command Line Interface (CLI) is a unified tool to manage your AWS services. With just one tool to download and…_aws.amazon.com](https://aws.amazon.com/cli "https://aws.amazon.com/cli")[](https://aws.amazon.com/cli)

*   **Dirsearch** — Search for directories with default wordlist and all (\*) extensions.

[**maurosoria/dirsearch**  
_dirsearch — Web path scanner_github.com](https://github.com/maurosoria/dirsearch "https://github.com/maurosoria/dirsearch")[](https://github.com/maurosoria/dirsearch)

**recon.rb** [**gist**](https://gist.github.com/ehsahil/f0f6e731a22a111399aa8503e34b6919)**.**

> **Usage: ruby recon.rb wordlist**

![Recon.rb demo run.](https://cdn-images-1.medium.com/max/800/1*SnV-UF4dxE1-iJoU6jcnlg.gif)
Recon.rb demo run.

A tool with Above functionality in the organized fashion.

**Lazyrecon**

[**nahamsec/lazyrecon**  
_lazyrecon — This script is intended to automate your reconnaissance process in an organized fashion_github.com](https://github.com/nahamsec/lazyrecon "https://github.com/nahamsec/lazyrecon")[](https://github.com/nahamsec/lazyrecon)

**Interesting blog posts**

[**\[BugBounty\] Decoding a $😱,000.00 htpasswd bounty**  
_A Private Bug Bounty Program had a globally readable .htpasswd file. I cracked the DES hash, got access to development…_blog.it-securityguard.com](https://blog.it-securityguard.com/bugbounty-decoding-a-%F0%9F%98%B1-00000-htpasswd-bounty/ "https://blog.it-securityguard.com/bugbounty-decoding-a-%F0%9F%98%B1-00000-htpasswd-bounty/")[](https://blog.it-securityguard.com/bugbounty-decoding-a-%F0%9F%98%B1-00000-htpasswd-bounty/)

[**Scanning the Alexa Top 1M for .DS\_Store files**  
_Some readers may remember our Analysis of .git folders in the Alexa Top 1M. WIth our tools, we were able to discover and…_en.internetwache.org](https://en.internetwache.org/scanning-the-alexa-top-1m-for-ds-store-files-12-03-2018/ "https://en.internetwache.org/scanning-the-alexa-top-1m-for-ds-store-files-12-03-2018/")[](https://en.internetwache.org/scanning-the-alexa-top-1m-for-ds-store-files-12-03-2018/)

### 3\. Visual Recon

I use the previously generated wordlist from subdomian.rb for visual recon.

I generally use the following two tools.

*   [**WebScreenshot**](https://github.com/maaaaz/webscreenshot)

[**maaaaz/webscreenshot**  
_webscreenshot — A simple script to screenshot a list of websites_github.com](https://github.com/maaaaz/webscreenshot "https://github.com/maaaaz/webscreenshot")[](https://github.com/maaaaz/webscreenshot)

![](https://cdn-images-1.medium.com/max/800/1*k_HXhIWo8TvbADiM_Skw-g.png)

*   [**Lazyshot**](https://github.com/mdhama/lazyshot)

[**mdhama/lazyshot**  
_lazyshot — The simplest way to take an automated screenshot of given URLs. Easy installation! Edit_github.com](https://github.com/mdhama/lazyshot "https://github.com/mdhama/lazyshot")[](https://github.com/mdhama/lazyshot)

![](https://cdn-images-1.medium.com/max/800/1*XnDnEykchL_PlM0Lt4146g.png)

**Interesting blog posts**

[**\[Tools\] Visual Recon — A beginners guide**  
_During the process of RECON you often get thousands of domains you have to look at. A suitable way to decrease the time…_blog.it-securityguard.com](https://blog.it-securityguard.com/visual-recon-a-beginners-guide/ "https://blog.it-securityguard.com/visual-recon-a-beginners-guide/")[](https://blog.it-securityguard.com/visual-recon-a-beginners-guide/)

### 4\. More Assets — More findings — More win.

I go for this section after reporting 2–3 issues in a particular program and wait for the response, if I find program interesting then I try to collect as much information as I can about the target using the following services.

*   **Censys**

[**Censys**  
_Censys is a platform that helps information security practitioners discover, monitor, and analyze devices that are…_censys.io](https://censys.io/ "https://censys.io/")[](https://censys.io/)

**Tool for Censys:**

[**yamakira/censys-enumeration**  
_censys-enumeration — A script to extract subdomains/emails for a given domain using SSL/TLS certificate dataset on…_github.com](https://github.com/yamakira/censys-enumeration "https://github.com/yamakira/censys-enumeration")[](https://github.com/yamakira/censys-enumeration)

*   **Shodan**

[**Shodan**  
_Shodan has servers located around the world that crawl the Internet 24/7 to provide the latest Internet intelligence…_www.shodan.io](https://www.shodan.io/ "https://www.shodan.io/")[](https://www.shodan.io/)

*   **ViewDNS** — Reverse Whois Lookup.

[**ViewDNS.info — Your one source for DNS related tools!**  
_Reverse IP Lookup Find all sites hosted on a given server._viewdns.info](http://viewdns.info/ "http://viewdns.info/")[](http://viewdns.info/)

Get the whois information of target using whois command or use an online tool.

> **whois domain.com**

If the company is not using Domain Privacy Service,

you will find the host-masters email address then use that email to find other domains registered on same email address using Reverse Whois Lookup. Targets Registered legal name also can be used.

![Result for hackeone inc query](https://cdn-images-1.medium.com/max/800/1*Z5xCr_GbcYYx2cNYfzSEKA.png)
Result for hackeone inc query

*   [**IP range Crawl**](https://bgp.he.net/)

![IP range for hackerone.com](https://cdn-images-1.medium.com/max/800/1*TkfmlFDVAFbL4Mn9JFQEbg.png)
IP range for hackerone.com

*   **AltDNS**

[**infosec-au/altdns**  
_altdns — Generates permutations, alterations and mutations of subdomains and then resolves them_github.com](https://github.com/infosec-au/altdns "https://github.com/infosec-au/altdns")[](https://github.com/infosec-au/altdns)

*   **Nmap Subdomain finding.**
*   **Content-Security-Policy (CSP)**

Tools

[**yamakira/domains-from-csp**  
_domains-from-csp — A script to extract domain names from Content Security Policy(CSP) headers_github.com](https://github.com/yamakira/domains-from-csp "https://github.com/yamakira/domains-from-csp")[](https://github.com/yamakira/domains-from-csp)

[**Analyse your HTTP response headers**  
_Quickly and easily assess the security of your HTTP response headers_securityheaders.com](https://securityheaders.com/ "https://securityheaders.com/")[](https://securityheaders.com/)

*   **More targets with Burp Suite** by  [**Jason Haddix**](https://medium.com/u/1dfc5adea2d4)

[Jason Haddix](https://medium.com/u/1dfc5adea2d4) Tweet about the method

*   **Domain Analyzer**

[**eldraco/domain\_analyzer**  
_domain\_analyzer — Analyze the security of any domain by finding all the information possible. Made in python._github.com](https://github.com/eldraco/domain_analyzer "https://github.com/eldraco/domain_analyzer")[](https://github.com/eldraco/domain_analyzer)

*   **Domain Profiler**

[**jpf/domain-profiler**  
_domain-profiler — Given a domain, will tell you the decisions that the domain owner has made._github.com](https://github.com/jpf/domain-profiler "https://github.com/jpf/domain-profiler")[](https://github.com/jpf/domain-profiler)

*   **VHost Scan**

[**codingo/VHostScan**  
_VHostScan — A virtual host scanner that performs reverse lookups, can be used with pivot tools, detect catch-all…_github.com](https://github.com/codingo/VHostScan "https://github.com/codingo/VHostScan")[](https://github.com/codingo/VHostScan)

*   **ThreatCrowd**

[**Threat Crowd | Threatcrowd.org Open Source Threat Intelligence**  
_© Copyright 2017 AlienVault, Inc. | AlienVault Products | AlienVault Solutions | Open Threat Exchange | Security…_www.threatcrowd.org](https://www.threatcrowd.org/ "https://www.threatcrowd.org/")[](https://www.threatcrowd.org/)

*   **Visual Site Mapper**

[**Visual Site Mapper — Create a visual map of your site**  
_Visual Site Mapper is a free service that can quickly show an interactive visual map of your site._www.visualsitemapper.com](http://www.visualsitemapper.com/ "http://www.visualsitemapper.com/")[](http://www.visualsitemapper.com/)

*   **Certificate Transparency**
*   **Google Transparency Report**

[**Google Transparency Report**  
_Edit description_transparencyreport.google.com](https://transparencyreport.google.com/https/certificates "https://transparencyreport.google.com/https/certificates")[](https://transparencyreport.google.com/https/certificates)

*   **Certsspotter**

[https://certspotter.com/api/v0/certs?domain=hackerone.com](https://certspotter.com/api/v0/certs?domain=domain.com)

*   **CertDB**

[**CertDB — SSL certificates search engine**  
_CertDB is a search engine for SSL certificates. It allows for exploration and analysis of data about organizations…_certdb.com](https://certdb.com/ "https://certdb.com/")[](https://certdb.com/)

*   **Crt.sh** —

[https://crt.sh/?q=%25domain.com](https://crt.sh/?q=%25domain.com)

*   **Facebook Certificate Transparency Monitoring Subscriptions.**

[**Certificate Transparency Monitoring — Facebook for Developers**  
_Edit description_developers.facebook.com](https://developers.facebook.com/tools/ct "https://developers.facebook.com/tools/ct")[](https://developers.facebook.com/tools/ct)

![Facebook Crt transparency monitoring subscriptions.](https://cdn-images-1.medium.com/max/800/1*KogNCTgMlSQmARkFplHBwA.png)
Facebook Crt transparency monitoring subscriptions.![Typical notification from Facebook when new asset on the same crt is available.](https://cdn-images-1.medium.com/max/800/1*dcLY8QxDdE88CoUlF1tHSg.png)
Typical notification from Facebook when new asset on the same crt is available.

**Interesting blog posts & tools taken from**

[**Asset Discovery: Doing Reconnaissance the Hard Way**  
_Last week, I wrote about Project Sonar as a great source for reconnaissance tasks. In this post, I want to generalize…_0xpatrik.com](https://0xpatrik.com/asset-discovery/ "https://0xpatrik.com/asset-discovery/")[](https://0xpatrik.com/asset-discovery/)

[**Subdomain Takeover: Thoughts on Risks**  
_Last year, I wrote about subdomain takeover. Although the concept is now generally understood, I noticed that people…_0xpatrik.com](https://0xpatrik.com/subdomain-takeover/ "https://0xpatrik.com/subdomain-takeover/")[](https://0xpatrik.com/subdomain-takeover/)

[**Subdomain Takeover: Proof Creation for Bug Bounties**  
_The post about subdomain takeover from last week received great feedback. I decided to follow-up and explain the…_0xpatrik.com](https://0xpatrik.com/takeover-proofs/ "https://0xpatrik.com/takeover-proofs/")[](https://0xpatrik.com/takeover-proofs/)

[**Project Sonar: An Underrated Source of Internet-wide Data**  
_The Internet-Wide Scans Data Repository (scans.io) was created alongside Censys. The purpose of this repository is to…_0xpatrik.com](https://0xpatrik.com/project-sonar-guide/ "https://0xpatrik.com/project-sonar-guide/")[](https://0xpatrik.com/project-sonar-guide/)

[**EdOverflow/can-i-take-over-xyz**  
_can-i-take-over-xyz — “Can I take over XYZ?” — a list of services and how to claim (sub)domains with dangling DNS…_github.com](https://github.com/EdOverflow/can-i-take-over-xyz "https://github.com/EdOverflow/can-i-take-over-xyz")[](https://github.com/EdOverflow/can-i-take-over-xyz)

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

[**AWS Command Line Interface**  
_The AWS Command Line Interface (CLI) is a unified tool to manage your AWS services. With just one tool to download and…_aws.amazon.com](https://aws.amazon.com/cli/ "https://aws.amazon.com/cli/")[](https://aws.amazon.com/cli/)

*   **Bucket Finder — **Great Tool for finding buckets using subdomains wordlist, can be integrated into recon.rb script but I don’t always use it.

[**Bucket Finder — DigiNinja**  
_An app to brute force Amazon S3 bucket names then search them for publicly available files. Even gives the option to…_digi.ninja](https://digi.ninja/projects/bucket_finder.php "https://digi.ninja/projects/bucket_finder.php")[](https://digi.ninja/projects/bucket_finder.php)

*   **LazyS3** — LazyS3 is an another tool which I use almost frequently to find the staging, sandboxed, dev and production buckets.

[**nahamsec/lazys3**  
_Contribute to lazys3 development by creating an account on GitHub._github.com](https://github.com/nahamsec/lazys3 "https://github.com/nahamsec/lazys3")[](https://github.com/nahamsec/lazys3)

*   **Slurp**: Slurp great tool for AWS Buckets Recon. (Deleted After Microsoft Purchased Github I guess). Weird!

[https://github.com/bbb31/slurp](https://github.com/bbb31/slurp)

*   **S3 Bucket Finder** — Another good tool for AWS S3 buckets.

[**gwen001/s3-buckets-finder**  
_s3-buckets-finder — Find aws s3 buckets and extract datas._github.com](https://github.com/gwen001/s3-buckets-finder "https://github.com/gwen001/s3-buckets-finder")[](https://github.com/gwen001/s3-buckets-finder)

**Interesting blog post**

[**A deep dive into AWS S3 access controls — taking full control over your assets**  
_TL;DR: Setting up access control of AWS S3 consists of multiple levels each with its own unique risk of…_labs.detectify.com](https://labs.detectify.com/2017/07/13/a-deep-dive-into-aws-s3-access-controls-taking-full-control-over-your-assets/ "https://labs.detectify.com/2017/07/13/a-deep-dive-into-aws-s3-access-controls-taking-full-control-over-your-assets/")[](https://labs.detectify.com/2017/07/13/a-deep-dive-into-aws-s3-access-controls-taking-full-control-over-your-assets/)

### 6\. Github For Recon.

Github is extremely helpful in finding Sensitive information regarding the targets. Access-keys, password, open endings, s3 buckets, backup files, etc. can be found on public GitHub repositories.

**Interesting blog post**

[**GitHub for Bug Bounty Hunters**  
_My tips for finding security issues in GitHub projects._edoverflow.com](https://edoverflow.com//2017/github-for-bugbountyhunters "https://edoverflow.com//2017/github-for-bugbountyhunters")[](https://edoverflow.com//2017/github-for-bugbountyhunters)

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

[**Online JavaScript beautifier**  
_Chrome, in case the built-in CSS and javascript formatting isn’t enough for you: — Quick source viewer by Tomi…_jsbeautifier.org](http://jsbeautifier.org/ "http://jsbeautifier.org/")[](http://jsbeautifier.org/)

The following tools are useful:

**LinkFinder**

[**GerbenJavado/LinkFinder**  
_LinkFinder — A python script that finds endpoints in JavaScript files_github.com](https://github.com/GerbenJavado/LinkFinder "https://github.com/GerbenJavado/LinkFinder")[](https://github.com/GerbenJavado/LinkFinder)

**JSParser** — Another great tool by [Behrouz Sadeghipour](https://medium.com/u/9a72584d6865)

[**nahamsec/JSParser**  
_Contribute to JSParser development by creating an account on GitHub._github.com](https://github.com/nahamsec/JSParser "https://github.com/nahamsec/JSParser")[](https://github.com/nahamsec/JSParser)

**Interesting blog post**

[**Bug Bounty — Tips / Tricks / JS (JavaScript Files)**  
_It all started in month of August when I reached out to Gerben Javado regarding a question, yes it was a basic question…_medium.com](https://medium.com/bugbountywriteup/bug-bounty-tips-tricks-js-javascript-files-bdde412ea49d "https://medium.com/bugbountywriteup/bug-bounty-tips-tricks-js-javascript-files-bdde412ea49d")[](https://medium.com/bugbountywriteup/bug-bounty-tips-tricks-js-javascript-files-bdde412ea49d)

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

Best of luck for all of your future infosec things.

If you have questions and anything about the post you want to ask me, Please contact me via twitter/fb. I’ll have my DM open.

Feedbacks and edits are welcome

[Twitter](https://twitter.com/ehsahil) [Facebook](https://fb.com/ehsahil)

Until next time!

**If you like my blog posts and my work, Please consider checking out my “Buy me a coffee” page**

[**Buy Me A Coffee - Best Way for Creators to Receive Tips**  
_Buy Me A Coffee help creators receive support from their audience in a friendly manner. Quickly accept donations and…_www.buymeacoffee.com](https://www.buymeacoffee.com/ehsahil "https://www.buymeacoffee.com/ehsahil")[](https://www.buymeacoffee.com/ehsahil)
