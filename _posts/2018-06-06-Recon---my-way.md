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

[**guelfoweb/knock** ](https://github.com/guelfoweb/knock "https://github.com/guelfoweb/knock")[](https://github.com/guelfoweb/knock)

*   [Sublist3r](https://github.com/aboul3la/Sublist3r)

[**aboul3la/Sublist3r** ](https://github.com/aboul3la/Sublist3r "https://github.com/aboul3la/Sublist3r")[](https://github.com/aboul3la/Sublist3r)

*   [Aquatone](https://github.com/michenriksen/aquatone)

[**michenriksen/aquatone** ](https://github.com/michenriksen/aquatone "https://github.com/michenriksen/aquatone")[](https://github.com/michenriksen/aquatone)

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

[**Nmap: the Network Mapper — Free Security Scanner** ](https://nmap.org/ "https://nmap.org/")[](https://nmap.org/)

*   **AWS CLI — **In the script AWS, CLI used test subdomains are connected to AWS bucket or not also checks for list permission. (Can be customized to test for write permission files.)

[**AWS Command Line Interface** ](https://aws.amazon.com/cli "https://aws.amazon.com/cli")[](https://aws.amazon.com/cli)

*   **Dirsearch** — Search for directories with default wordlist and all (\*) extensions.

[**maurosoria/dirsearch**  ](https://github.com/maurosoria/dirsearch "https://github.com/maurosoria/dirsearch")[](https://github.com/maurosoria/dirsearch)

**recon.rb** [**gist**](https://gist.github.com/ehsahil/f0f6e731a22a111399aa8503e34b6919)**.**

> **Usage: ruby recon.rb wordlist**

![Recon.rb demo run.](https://cdn-images-1.medium.com/max/800/1*SnV-UF4dxE1-iJoU6jcnlg.gif)
Recon.rb demo run.

A tool with Above functionality in the organized fashion.

**Lazyrecon**

[**nahamsec/lazyrecon** ](https://github.com/nahamsec/lazyrecon "https://github.com/nahamsec/lazyrecon")[](https://github.com/nahamsec/lazyrecon)

**Interesting blog posts**

[**\[BugBounty\] Decoding a $😱,000.00 htpasswd bounty** ](https://blog.it-securityguard.com/bugbounty-decoding-a-%F0%9F%98%B1-00000-htpasswd-bounty/ "https://blog.it-securityguard.com/bugbounty-decoding-a-%F0%9F%98%B1-00000-htpasswd-bounty/")[](https://blog.it-securityguard.com/bugbounty-decoding-a-%F0%9F%98%B1-00000-htpasswd-bounty/)

[**Scanning the Alexa Top 1M for .DS\_Store files** ](https://en.internetwache.org/scanning-the-alexa-top-1m-for-ds-store-files-12-03-2018/ "https://en.internetwache.org/scanning-the-alexa-top-1m-for-ds-store-files-12-03-2018/")[](https://en.internetwache.org/scanning-the-alexa-top-1m-for-ds-store-files-12-03-2018/)

### 3\. Visual Recon

I use the previously generated wordlist from subdomian.rb for visual recon.

I generally use the following two tools.

*   [**maaaaz/webscreenshot** ](https://github.com/maaaaz/webscreenshot "https://github.com/maaaaz/webscreenshot")[](https://github.com/maaaaz/webscreenshot)

![](https://cdn-images-1.medium.com/max/800/1*k_HXhIWo8TvbADiM_Skw-g.png)

*   [**mdhama/lazyshot** ](https://github.com/mdhama/lazyshot "https://github.com/mdhama/lazyshot")[](https://github.com/mdhama/lazyshot)

![](https://cdn-images-1.medium.com/max/800/1*XnDnEykchL_PlM0Lt4146g.png)

**Interesting blog posts**

[**\[Tools\] Visual Recon — A beginners guide** ](https://blog.it-securityguard.com/visual-recon-a-beginners-guide/ "https://blog.it-securityguard.com/visual-recon-a-beginners-guide/")[](https://blog.it-securityguard.com/visual-recon-a-beginners-guide/)

### 4\. More Assets — More findings — More win.

I go for this section after reporting 2–3 issues in a particular program and wait for the response, if I find program interesting then I try to collect as much information as I can about the target using the following services.


[**Censys** ](https://censys.io/ "https://censys.io/")[](https://censys.io/)

**Tool for Censys:**

[**yamakira/censys-enumeration** ](https://github.com/yamakira/censys-enumeration "https://github.com/yamakira/censys-enumeration")[](https://github.com/yamakira/censys-enumeration)

*  [**Shodan** ](https://www.shodan.io/ "https://www.shodan.io/")[](https://www.shodan.io/)



*   [**ViewDNS.info — Your one source for DNS related tools!**  ](http://viewdns.info/ "http://viewdns.info/")[](http://viewdns.info/)



Get the whois information of target using whois command or use an online tool.

> **whois domain.com**

If the company is not using Domain Privacy Service,

you will find the host-masters email address then use that email to find other domains registered on same email address using Reverse Whois Lookup. Targets Registered legal name also can be used.

![Result for hackeone inc query](https://cdn-images-1.medium.com/max/800/1*Z5xCr_GbcYYx2cNYfzSEKA.png)


*   [**IP range Crawl**](https://bgp.he.net/)

![IP range for hackerone.com](https://cdn-images-1.medium.com/max/800/1*TkfmlFDVAFbL4Mn9JFQEbg.png)
IP range for hackerone.com

*   [**infosec-au/altdns** ](https://github.com/infosec-au/altdns "https://github.com/infosec-au/altdns")[](https://github.com/infosec-au/altdns)


*   **Nmap Subdomain finding.**
*   **Content-Security-Policy (CSP)**

Tools

[**yamakira/domains-from-csp**  ](https://github.com/yamakira/domains-from-csp "https://github.com/yamakira/domains-from-csp")[](https://github.com/yamakira/domains-from-csp)

[**Analyse your HTTP response headers** ](https://securityheaders.com/ "https://securityheaders.com/")[](https://securityheaders.com/)


*   [**eldraco/domain\_analyzer** ](https://github.com/eldraco/domain_analyzer "https://github.com/eldraco/domain_analyzer")[](https://github.com/eldraco/domain_analyzer)



*   [**jpf/domain-profiler**  ](https://github.com/jpf/domain-profiler "https://github.com/jpf/domain-profiler")[](https://github.com/jpf/domain-profiler)


*   [**codingo/VHostScan** ](https://github.com/codingo/VHostScan "https://github.com/codingo/VHostScan")[](https://github.com/codingo/VHostScan)


*  [**Visual Site Mapper — Create a visual map of your site** ](http://www.visualsitemapper.com/ "http://www.visualsitemapper.com/")[](http://www.visualsitemapper.com/)



*   **Certificate Transparency**

[**Google Transparency Report** ](https://transparencyreport.google.com/https/certificates "https://transparencyreport.google.com/https/certificates")[](https://transparencyreport.google.com/https/certificates)

*   [https://certspotter.com/api/v0/certs?domain=hackerone.com](https://certspotter.com/api/v0/certs?domain=domain.com)


*   [**CertDB — SSL certificates search engine** ](https://certdb.com/ "https://certdb.com/")[](https://certdb.com/)



*   [https://crt.sh/?q=%25domain.com](https://crt.sh/?q=%25domain.com)



*   [**Certificate Transparency Monitoring — Facebook for Developers** ](https://developers.facebook.com/tools/ct "https://developers.facebook.com/tools/ct")[](https://developers.facebook.com/tools/ct)



![Facebook Crt transparency monitoring subscriptions.](https://cdn-images-1.medium.com/max/800/1*KogNCTgMlSQmARkFplHBwA.png)
Facebook Crt transparency monitoring subscriptions.

![Typical notification from Facebook when new asset on the same crt is available.](https://cdn-images-1.medium.com/max/800/1*dcLY8QxDdE88CoUlF1tHSg.png)
Typical notification from Facebook when new asset on the same crt is available.

**Interesting blog posts & tools taken from**

[**Asset Discovery: Doing Reconnaissance the Hard Way**  ](https://0xpatrik.com/asset-discovery/ "https://0xpatrik.com/asset-discovery/")[](https://0xpatrik.com/asset-discovery/)

[**Subdomain Takeover: Thoughts on Risks**  ](https://0xpatrik.com/subdomain-takeover/ "https://0xpatrik.com/subdomain-takeover/")[](https://0xpatrik.com/subdomain-takeover/)

[**Subdomain Takeover: Proof Creation for Bug Bounties** ](https://0xpatrik.com/takeover-proofs/ "https://0xpatrik.com/takeover-proofs/")[](https://0xpatrik.com/takeover-proofs/)

[**Project Sonar: An Underrated Source of Internet-wide Data**  ](https://0xpatrik.com/project-sonar-guide/ "https://0xpatrik.com/project-sonar-guide/")[](https://0xpatrik.com/project-sonar-guide/)

[**EdOverflow/can-i-take-over-xyz**  ](https://github.com/EdOverflow/can-i-take-over-xyz "https://github.com/EdOverflow/can-i-take-over-xyz")[](https://github.com/EdOverflow/can-i-take-over-xyz)

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



*   [https://github.com/bbb31/slurp](https://github.com/bbb31/slurp) - Slurp great tool for AWS Buckets Recon. (Deleted After Microsoft Purchased Github I guess). Weird!



*   
[**gwen001/s3-buckets-finder**  ](https://github.com/gwen001/s3-buckets-finder "https://github.com/gwen001/s3-buckets-finder")[](https://github.com/gwen001/s3-buckets-finder)— Another good tool for AWS S3 buckets.


**Interesting blog post**

[**A deep dive into AWS S3 access controls — taking full control over your assets** ](https://labs.detectify.com/2017/07/13/a-deep-dive-into-aws-s3-access-controls-taking-full-control-over-your-assets/ "https://labs.detectify.com/2017/07/13/a-deep-dive-into-aws-s3-access-controls-taking-full-control-over-your-assets/")[](https://labs.detectify.com/2017/07/13/a-deep-dive-into-aws-s3-access-controls-taking-full-control-over-your-assets/)

### 6\. Github For Recon.

Github is extremely helpful in finding Sensitive information regarding the targets. Access-keys, password, open endings, s3 buckets, backup files, etc. can be found on public GitHub repositories.

**Interesting blog post**

[**GitHub for Bug Bounty Hunters**  ](https://edoverflow.com//2017/github-for-bugbountyhunters "https://edoverflow.com//2017/github-for-bugbountyhunters")[](https://edoverflow.com//2017/github-for-bugbountyhunters)

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

[**Online JavaScript beautifier**  ](http://jsbeautifier.org/ "http://jsbeautifier.org/")[](http://jsbeautifier.org/)

The following tools are useful:

* [**GerbenJavado/LinkFinder**  ](https://github.com/GerbenJavado/LinkFinder "https://github.com/GerbenJavado/LinkFinder")[](https://github.com/GerbenJavado/LinkFinder)



* [**nahamsec/JSParser**  ](https://github.com/nahamsec/JSParser "https://github.com/nahamsec/JSParser")[](https://github.com/nahamsec/JSParser)


**Interesting blog post**

[**Bug Bounty — Tips / Tricks / JS (JavaScript Files)**  ](https://medium.com/bugbountywriteup/bug-bounty-tips-tricks-js-javascript-files-bdde412ea49d "https://medium.com/bugbountywriteup/bug-bounty-tips-tricks-js-javascript-files-bdde412ea49d")[](https://medium.com/bugbountywriteup/bug-bounty-tips-tricks-js-javascript-files-bdde412ea49d)

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

[**Buy Me A Coffee - Best Way for Creators to Receive Tips** ](https://www.buymeacoffee.com/ehsahil "https://www.buymeacoffee.com/ehsahil")[](https://www.buymeacoffee.com/ehsahil)
