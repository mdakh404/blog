---
title: >-
  Data Breaches are on the Rise — Is it too hard to p̶r̶e̶v̶e̶n̶t̶ control data
  breaches?
description: >-
  Recent widely publicized data breaches have exposed the personal information
  of hundreds of millions of people. Some reports point to…
date: '2019-07-02T14:59:47.211Z'
categories: []
keywords: []
slug: >-
  /@ehsahil/data-breaches-are-on-the-rise-is-it-too-hard-to-p%CC%B6r%CC%B6e%CC%B6v%CC%B6e%CC%B6n%CC%B6t%CC%B6-control-data-breaches-c32dc563bb5
---

Recent widely publicized data breaches have exposed the personal information of hundreds of millions of people. Some reports point to alarming increases in both the size and frequency of data breaches. Also, there are two types of breaches:-

*   One, which you know and is public.
*   Second, which you actually don’t come to know because data was never put on Dark web but it was actually used by attackers for personal gain.

In April 2019 @haveibeenpwned reported 8 public new breaches -

![](https://cdn-images-1.medium.com/max/800/1*XRemOhwvyTcONt9CgI9ofw.png)

**Most common causes of a data breach?**

*   #1 Weak and Stolen Credentials, a.k.a. Passwords
*   #2 Old, Unpatched Security Vulnerabilities
*   #3 Application level Vulnerabilities
*   #4 Improper Configuration at Network/Infra Level
*   #5 Social Engineering
*   #6 Human Negligence / Error
*   #7 Insider Threats

Mistakes happen and errors are made but it’s important to learn from those mistakes and never repeat them again. The key point to note:

> **Security is not a one time process, it’s a continuous process.**

There is nothing like 100% secure,  there are always some security loopholes, it’s important to identify them, patch them and repeat the process.

> **you have to be lucky every time but the attacker needs to be lucky only once**

### Effective ways to control data breaches:

1.  **Assets Management**

1.1 — Mapping your external surface

1.2 — Identify and Assess

1.3 — Monitoring external surface.

**2\. Code Review / Deployment Review**

2.1 — Static and Dynamic code review

2.2 — Read your Javascript files

**3\. Organization Secrets Monitor**

3.1 — Publicly Disclosed Sensitive Information

3.2 — Monitoring Breaches

**4\. Internal Practices**

4.1 — Two/Multi-Factor Authentication

4.2 — Security Practices: Off Boarding / On-Boarding

4.3 — Employee Security Training

4.4 — Employee’s Personal Security Checklist

4.5 — Sharing Sensitive Information Internally (Hosted Pastebin Solution)

4.6 — Limiting Staging / Development Server in Restricted IPs / Proxy

4.7 — Cloud Infrastructure Security.

4.8 — Making Engineering Team Active in InfoSec

4.9 — Logging and Monitoring

**5\. Best Practices — Responsible Disclosure**

5.1 — Security.txt

5.2 — Responsible Disclosure Policy

**6\. Last but not least…..**

6.1 — Follow cool guys on Twitter.

6.2 — Go Hack yourself — Detectify

6.3 — Best Security Checklists out there.

6.4 — Awesome Incident Response

6.5 — Awesome Threat Detection & intelligence

### **1\. Assets Management**

I’ve seen companies do not even have the proper information about all the services they are using. It’s really important to have the assets inventory. Monitoring of the assets from the assets inventory.

#### If You’re Not Doing Continuous Asset Management You’re Not Doing Security — Daniel Miessler

[**If You’re Not Doing Continuous Asset Management You’re Not Doing Security | Daniel Miessler**  
_The more a company can tell me about their assets the better their security is, and the more comprehensive and realtime…_danielmiessler.com](https://danielmiessler.com/blog/continuous-asset-management-security/ "https://danielmiessler.com/blog/continuous-asset-management-security/")[](https://danielmiessler.com/blog/continuous-asset-management-security/)

Continuous Monitoring of your External Surface is very important than you think.

#### 1.1 — Mapping your external surface.

**OSINT** — Collecting data regarding your company using Open source intelligence tools. OSINT plays a very important role in giving whole insight into the companies at a relatively lower cost. OSINT uses publicly available sources together with the important data related to your organization.

[**Recon — my way.**  
_A detailed blog post on my reconnaissance processes for web applications security testing. I always wanted to write…_medium.com](https://medium.com/@ehsahil/recon-my-way-82b7e5f62e21 "https://medium.com/@ehsahil/recon-my-way-82b7e5f62e21")[](https://medium.com/@ehsahil/recon-my-way-82b7e5f62e21)

[**Subdomain Enumeration: 2019 Workflow**  
_You are probably shaking your head that this is another post about subdomain enumeration. I have written about it in…_0xpatrik.com](https://0xpatrik.com/subdomain-enumeration-2019/ "https://0xpatrik.com/subdomain-enumeration-2019/")[](https://0xpatrik.com/subdomain-enumeration-2019/)

[**jivoi/awesome-osint**  
_scream: A curated list of amazingly awesome OSINT - jivoi/awesome-osint_github.com](https://github.com/jivoi/awesome-osint "https://github.com/jivoi/awesome-osint")[](https://github.com/jivoi/awesome-osint)

[**Ph055a/OSINT-Collection**  
_Maintained collection of OSINT related resources. (All Free & Actionable) - Ph055a/OSINT-Collection_github.com](https://github.com/Ph055a/OSINT-Collection "https://github.com/Ph055a/OSINT-Collection")[](https://github.com/Ph055a/OSINT-Collection)

[**Shodan**](https://shodan.io) — Shodan is a search engine that lets the user find specific types of computers connected to the internet using a variety of filters.

![](https://cdn-images-1.medium.com/max/800/1*NZcmzHWzhVq803SQ-Stm_A.png)

[**Censys**](https://censys.io) — find and monitor every server on the internet.

![](https://cdn-images-1.medium.com/max/800/1*c0XqedA1nqGhufTezqtXVQ.png)

#### 1.2 — Identify and Assess

The Critical part of the application and data and audit it for security vulnerabilities. For auditing, you can hire someone internally or you can also outsource the work to a reputable security service provider. do a regular security assessment of the critical part of the applications.

Generally, the different part of the application has a different kind of vulnerabilities, we need to identify the part of the application with respect to the risk associated with them.

The security strength is determined by the security of the weakest part of the application.

The part of the application exposed to the public is the weakest part, the external surface should always be on priority.

[**An Expert Guide to Securing Sensitive Data: 34 Experts Reveal the Biggest Mistakes Companies Make…**  
_We asked 34 experts what the biggest mistakes companies make with data security are. Here's what they had to say…_digitalguardian.com](https://digitalguardian.com/blog/expert-guide-securing-sensitive-data-34-experts-reveal-biggest-mistakes-companies-make-data "https://digitalguardian.com/blog/expert-guide-securing-sensitive-data-34-experts-reveal-biggest-mistakes-companies-make-data")[](https://digitalguardian.com/blog/expert-guide-securing-sensitive-data-34-experts-reveal-biggest-mistakes-companies-make-data)

#### **1.3 — Continuous monitoring of your External surface.**

[**Continuous Asset Management and Cybersecurity: How We Got Here and Where We’re Going**  
_In a widely shared article by Daniel Miessler and a post by Anton Chuvakin, the topic of asset management and its…_medium.com](https://medium.com/axonius/continuous-asset-management-and-cybersecurity-how-we-got-here-and-where-were-going-6d0856001058 "https://medium.com/axonius/continuous-asset-management-and-cybersecurity-how-we-got-here-and-where-were-going-6d0856001058")[](https://medium.com/axonius/continuous-asset-management-and-cybersecurity-how-we-got-here-and-where-were-going-6d0856001058)

[**yassineaboukir/sublert**  
_Sublert is a security and reconnaissance tool which leverages certificate transparency to automatically monitor new…_github.com](https://github.com/yassineaboukir/sublert "https://github.com/yassineaboukir/sublert")[](https://github.com/yassineaboukir/sublert)

You can create your own slack bots to notify you whenever new subdomain popup in added public sources. uses of slack bots are limitless.

### **2 — Code Review / Deployment Review**

Doing manual testing for your application is very important but we cannot do the manual testing when there are thousands of lines of code deployed every day, for overall security Approach, you have to include security components into your development cycle. This includes static and dynamic code review.

Secure Development cycle with security components

Developers write code → Passed through static code analyzer → Passed though sensitive information disclosure tools → Passed open source vulnerability scanner → deployment to the staging server → Manual testing using proxy tools, (Create checklist according to the business requirement. ) → PRODUCTION.

[**Automated Security Testing for Developers**  
_Continuous separate testing that ensures that new commits and builds don’t introduce security problems is an essential…_medium.com](https://medium.com/@cossacklabs/automated-security-testing-56ee1253c1fd "https://medium.com/@cossacklabs/automated-security-testing-56ee1253c1fd")[](https://medium.com/@cossacklabs/automated-security-testing-56ee1253c1fd)

#### 2.1 — Static and Dynamics code review

Implementation of the Static code analyzer in your pipeline. The static code analyzer tools collect the information based on the source code provided.

[**Continuous Inspection | SonarQube**  
_The leading product for continuous code quality_www.sonarqube.org](https://www.sonarqube.org/ "https://www.sonarqube.org/")[](https://www.sonarqube.org/)

[**RIPS — free PHP security scanner using static code analysis**  
_RIPS is a free and open source PHP security scanner using static code analysis to find security vulnerabilities in PHP…_rips-scanner.sourceforge.net](http://rips-scanner.sourceforge.net/ "http://rips-scanner.sourceforge.net/")[](http://rips-scanner.sourceforge.net/)

#### **2.2 — Read your public Javascript files**

Don’t hardcode your sensitive keys/data/login in javascript.

Scan your javascript files for sensitive paths and information hard-coded.

[**nahamsec/JSParser**  
_Contribute to nahamsec/JSParser development by creating an account on GitHub._github.com](https://github.com/nahamsec/JSParser "https://github.com/nahamsec/JSParser")[](https://github.com/nahamsec/JSParser)

[**GerbenJavado/LinkFinder**  
_A python script that finds endpoints in JavaScript files — GerbenJavado/LinkFinder_github.com](https://github.com/GerbenJavado/LinkFinder "https://github.com/GerbenJavado/LinkFinder")[](https://github.com/GerbenJavado/LinkFinder)

### 3 — Organization Secret Monitor

#### 3.1 — Publicly disclosed Sensitive Information

It is very important to define the keywords related to your organization, this could include the domains externally and internally your team is using. you can use your defined keywords to see what things have been publicly posted.

The following blog post lists the common keywords used by the Bug bounty hunter or hackers in general to find sensitive information related to your organization.

[**GitHub for Bug Bounty Hunters**  
_My tips for finding security issues in GitHub projects._edoverflow.com](https://edoverflow.com/2017/github-for-bugbountyhunters/ "https://edoverflow.com/2017/github-for-bugbountyhunters/")[](https://edoverflow.com/2017/github-for-bugbountyhunters/)

Monitor what your employee posted on Public channels like, Github, Pastebin, etc

You can use the following tools to scan your code if you have hardcoded any sensitive information.

[**zricethezav/gitleaks**  
_Audit git repos for secrets 🔑. Contribute to zricethezav/gitleaks development by creating an account on GitHub._github.com](https://github.com/zricethezav/gitleaks "https://github.com/zricethezav/gitleaks")[](https://github.com/zricethezav/gitleaks)

[**michenriksen/gitrob**  
_Reconnaissance tool for GitHub organizations. Contribute to michenriksen/gitrob development by creating an account on…_github.com](https://github.com/michenriksen/gitrob "https://github.com/michenriksen/gitrob")[](https://github.com/michenriksen/gitrob)

[**dxa4481/truffleHog**  
_Searches through git repositories for high entropy strings and secrets, digging deep into commit history …_github.com](https://github.com/dxa4481/truffleHog "https://github.com/dxa4481/truffleHog")[](https://github.com/dxa4481/truffleHog)

#### 3.2 — Monitoring Breaches

Breaches happen every day and you should know about every breach where your or your organization's data is compromised.

[**How to monitor your data breach exposure**  
_If you’re not yet monitoring your data breach exposure, I really advice you start doing it now. If you’re already doing…_medium.com](https://medium.com/@john.opdenakker/how-to-monitor-your-data-breach-exposure-a8cc959431bb "https://medium.com/@john.opdenakker/how-to-monitor-your-data-breach-exposure-a8cc959431bb")[](https://medium.com/@john.opdenakker/how-to-monitor-your-data-breach-exposure-a8cc959431bb)

Subscribe on Have I been Pwned using your [security@company.com](mailto:security@company.com)

**‘; — have I been pwned?**

[https://haveibeenpwned.co](https://haveibeenpwned.com/)m

![](https://cdn-images-1.medium.com/max/800/1*55aMa4q_P8N2qKfT9GZg-A.png)

**Firefox Monitor**

[**Find out if you've been part of a data breach**  
_Find out if you've been part of a data breach with Firefox Monitor. Sign up for alerts about future breaches and get…_monitor.firefox.com](https://monitor.firefox.com "https://monitor.firefox.com")[](https://monitor.firefox.com)

![](https://cdn-images-1.medium.com/max/800/1*Obr00Z8gc5L36gjjGzBRmQ.png)

### **4 — Internal Practices**

#### 4.1 — 2FA/Multi-Factor Authentication

Use 2-Factor Authentication on every 3rd party services you are using including Gsuite, GitHub, Gitlab, etc and cloud service providers.

[**Two-Factor Authentication for Beginners**  
_Passwords are the brittle wall that keep unwanted visitors out of your accounts. When it comes to account protection…_medium.com](https://medium.com/@mshelton/two-factor-authentication-for-beginners-b29b0eec07d7 "https://medium.com/@mshelton/two-factor-authentication-for-beginners-b29b0eec07d7")[](https://medium.com/@mshelton/two-factor-authentication-for-beginners-b29b0eec07d7)

The following services must have enabled the 2FA for everyone at the company.

*   Google Services — Gsuite, Gmail, etc
*   Github, Gitlab, Atlassian
*   Cloud Service providers — AWS, Google Cloud, Azure, Alibaba cloud, etc.
*   Companies official social media platforms — Twitter, Facebook, Youtube, etc

#### 4.2 — Security Practices: On-Boarding / Off Boarding

Secure onboarding and offboarding is very important for an organization,

**Onboarding —**

When a new employee enters an organization there are various behind-the-scenes activities that must take place to ensure the new hire efficient onboarding experience. Many are administrative in nature and are taken care of by HR.

But then there are those related to cybersecurity — and they are far too often overlooked.

**Offboarding —**

Companies often do a good job of monitoring and controlling employees tech use on the job, but need to better evaluate vulnerabilities in their offboarding process with an eye toward protecting organizational data and resources.

Remove their access to the Internal systems ASAP and rotate credentials they might have access to.

[**Management**  
_Managing users across departments and locations can be a nightmare. Explore some of the more common challenges and…_www.intermedia.net](https://www.intermedia.net/it-challenges/management/best-practices-onboarding-offboarding-employees "https://www.intermedia.net/it-challenges/management/best-practices-onboarding-offboarding-employees")[](https://www.intermedia.net/it-challenges/management/best-practices-onboarding-offboarding-employees)

#### **4.3 — Employee Security Training**

Security Training for everyone in the organization.

[**For Everyone - PagerDuty Security Training**  
_This is an open-source version of 'Security Training for Everyone', PagerDuty's internal employee security training…_sudo.pagerduty.com](https://sudo.pagerduty.com/for_everyone/ "https://sudo.pagerduty.com/for_everyone/")[](https://sudo.pagerduty.com/for_everyone/)

Security training for Engineers.

[**For Engineers - PagerDuty Security Training**  
_This is an open-source version of 'Security Training for Engineers', PagerDuty's internal employee technical security…_sudo.pagerduty.com](https://sudo.pagerduty.com/for_engineers/ "https://sudo.pagerduty.com/for_engineers/")[](https://sudo.pagerduty.com/for_engineers/)

Setting up Guidelines for Engineers for secure software development, you can take reference from the below repo.

[**alulsh/intro-to-security-for-developers**  
_An introduction to security for developers. Contribute to alulsh/intro-to-security-for-developers development by…_github.com](https://github.com/alulsh/intro-to-security-for-developers "https://github.com/alulsh/intro-to-security-for-developers")[](https://github.com/alulsh/intro-to-security-for-developers)

[**Security Resources for Software Teams | Sqreen**  
_Sqreen is a SaaS platform which automatically protects your web applications, in 30 seconds, with no code modification._www.sqreen.com](https://www.sqreen.com/resources "https://www.sqreen.com/resources")[](https://www.sqreen.com/resources)

#### 4.4 — Employee’s Personal Security Checklist

[**alulsh/personal-security-checklist**  
_Personal security checklist for securing your devices and accounts. — alulsh/personal-security-checklist_github.com](https://github.com/alulsh/personal-security-checklist "https://github.com/alulsh/personal-security-checklist")[](https://github.com/alulsh/personal-security-checklist)

During Induction you can provide information on how we do Security at our organization and how you can contribute to it and how to do your work in a secure way.

#### 4.5 — Sharing Sensitive Internally (Hosted Pastebin Solution)

Don’t share the credentials/secrets etc via slack, hangout, WhatsApp, etc use a tool — **Privatebin** to share the credentials/secrets internally.

[**PrivateBin**  
_General information on the PrivateBin project._privatebin.info](https://privatebin.info/ "https://privatebin.info/")[](https://privatebin.info/)

#### 4.6 — Limiting Staging / Development Server in Restricted IPs / Proxy

Make all your non-prod and staging environment behind the VPN Only. you can use the Open source VPN Pritunl.

[**Enterprise VPN Server**  
_Free open source enterprise distributed VPN server. Virtualize your private networks across datacenters and provide…_pritunl.com](https://pritunl.com/ "https://pritunl.com/")[](https://pritunl.com/)

Know about your assets before someone else does, build your own monitoring system.

**4.7 — Cloud Infrastructure Security.**

Organizations are more and more going for the cloud infrastructure because it has numerous benefits over the traditional way.

Amazon web services are the leader in the cloud infrastructure providers and let's discuss best practices for AWS

1.  Enable 2FA for your AWS account.
2.  You can allow login to your AWS console from some specific IP’s only.
3.  Make sure your database is not reachable from outside.
4.  Don’t provide the access more than required. Control it using IAM policies.

Cloud provider provided all the options and features to secure themselves but due to the carelessness of a single individual, it could lead to disaster for the whole organization.

[**Cloud security: The essential checklist**  
_Cloud security is one of those things that everyone knows they need, but few people understand how to deal with. I The…_www.infoworld.com](https://www.infoworld.com/article/3321757/cloud-security-the-essential-checklist.html "https://www.infoworld.com/article/3321757/cloud-security-the-essential-checklist.html")[](https://www.infoworld.com/article/3321757/cloud-security-the-essential-checklist.html)

[**2016 Data Security Incident | Uber Newsroom US**  
_As Uber’s CEO, it’s my job to set our course for the future, which begins with building a company that every Uber…_www.uber.com](https://www.uber.com/newsroom/2016-data-incident/ "https://www.uber.com/newsroom/2016-data-incident/")[](https://www.uber.com/newsroom/2016-data-incident/)

[**How DJI fumbled its bug bounty program and created a PR nightmare**  
_Written by Chris Bing Nov 30, 2017 | CYBERSCOOP A software vulnerability disclosure program recently launched by…_www.cyberscoop.com](https://www.cyberscoop.com/dji-bug-bounty-drone-technology-sean-melia-kevin-finisterre/ "https://www.cyberscoop.com/dji-bug-bounty-drone-technology-sean-melia-kevin-finisterre/")[](https://www.cyberscoop.com/dji-bug-bounty-drone-technology-sean-melia-kevin-finisterre/)

**Scout2 by NCC group for AWS**

[**nccgroup/Scout2**  
_Security auditing tool for AWS environments. Contribute to nccgroup/Scout2 development by creating an account on…_github.com](https://github.com/nccgroup/Scout2 "https://github.com/nccgroup/Scout2")[](https://github.com/nccgroup/Scout2)

#### 4.8 — Making Engineering Team Active in InfoSec

Create a technology group or security group and add your team members in there and share information related to Information security.

Identify an individual from the team who has better knowledge when it comes to security and is passionate enough to learn something new. Make them lead the security piece within their team. It will help in bringing up the awareness and the team will only get stronger.

#### 4.9 — Logging and monitoring —

Currently, lack of Logging and monitoring is the #10 vulnerability in latest OWASP top 10 most critical vulnerabilities.

**Nagios** — Nagios provides complete monitoring of security logs and security data — including access logs, audit logs, application logs, log files, event logs, service logs, and system logs on Windows servers, Linux servers, and Unix servers

[**Security Log Monitoring — Nagios**  
_Nagios provides complete monitoring of security logs and security data — including access logs, audit logs, application…_www.nagios.com](https://www.nagios.com/solutions/security-log-monitoring/ "https://www.nagios.com/solutions/security-log-monitoring/")[](https://www.nagios.com/solutions/security-log-monitoring/)

**Gauntlt** — Go Ahead, Be Mean To Your Code — Security and Rugged Testing

[**GAUNTLT — Go Ahead, Be Mean To Your Code — Security and Rugged Testing**  
_Gauntlt provides hooks to a variety of security tools and puts them within reach of security, dev and ops teams to…_gauntlt.org](http://gauntlt.org/ "http://gauntlt.org/")[](http://gauntlt.org/)

**Kibana** — Kibana lets you visualize your Elasticsearch data and navigate the Elastic Stack, so you can do anything from learning why you’re getting paged at 2:00 a.m. to understanding the impact rain might have on your quarterly numbers.

[**Kibana: Explore, Visualize, Discover Data | Elastic**  
_Download Kibana or the complete Elastic Stack for free and start visualizing, analyzing, and exploring your data with…_www.elastic.co](https://www.elastic.co/products/kibana "https://www.elastic.co/products/kibana")[](https://www.elastic.co/products/kibana)

[**Logging and Monitoring**  
_Information technology drives productivity and growth in almost every industry today. One computing device contains…_resources.infosecinstitute.com](https://resources.infosecinstitute.com/category/certifications-training/cissp/domains/security-operations/logging-and-monitoring/#gref "https://resources.infosecinstitute.com/category/certifications-training/cissp/domains/security-operations/logging-and-monitoring/#gref")[](https://resources.infosecinstitute.com/category/certifications-training/cissp/domains/security-operations/logging-and-monitoring/#gref)

### **5 — Best Practices — Responsible Disclosure**

#### 5.1 — Security.txt

A proposed standard which allows websites to define security policies.

Implementation of the security.txt, as robots.txt is for the bots and search engines similarly the security.txt is for external security researchers and bug bounty. the companies should provide a secure way to responsibly disclose the vulnerability anyone found intentionally or unintentionally.

[**security.txt**  
_A proposed standard which allows websites to define security policies._securitytxt.org](https://securitytxt.org/ "https://securitytxt.org/")[](https://securitytxt.org/)

#### 5.2 — Responsible Disclosure Policy

Having a responsible disclosure program is a must. It’s not always necessary to start with a bounty program, having a VDP helps an organization to get reports from researchers who might have knowingly or unknowingly stumbled upon something which you would like to know. After which you can investigate and decide if you would like to make a payout to the researching for his finding.

[**Vulnerability Disclosure Policy Basics: 5 Critical Components**  
_In July 2017, the Dept of Justice issued a framework for organizations looking to implement vulnerability disclosure…_www.hackerone.com](https://www.hackerone.com/blog/Vulnerability-Disclosure-Policy-Basics-5-Critical-Components "https://www.hackerone.com/blog/Vulnerability-Disclosure-Policy-Basics-5-Critical-Components")[](https://www.hackerone.com/blog/Vulnerability-Disclosure-Policy-Basics-5-Critical-Components)

[**What is Responsible Disclosure? | Bugcrowd**  
_Benefit from the knowledge of security researchers by providing them transparent rules for submitting vulnerabilities…_www.bugcrowd.com](https://www.bugcrowd.com/resource/what-is-responsible-disclosure/ "https://www.bugcrowd.com/resource/what-is-responsible-disclosure/")[](https://www.bugcrowd.com/resource/what-is-responsible-disclosure/)

### 6 — Last but not least…..

**6.1 — Be active in the infosec community — follow cool security guys.**

**6.2 — Go Hack yourself — Detectify**

[**The Web Application Hacker’s Handbook**  
_For over a decade, The Web Application Hacker’s Handbook (WAHH) has been the de facto standard reference book for…_portswigger.net](https://portswigger.net/web-security/web-application-hackers-handbook "https://portswigger.net/web-security/web-application-hackers-handbook")[](https://portswigger.net/web-security/web-application-hackers-handbook)

[**Basic Penetration testing lab — 1**  
_I am setting up a new lab for me and thought to document the process, so anyone wants to do the same can take…_medium.com](https://medium.com/@ehsahil/basic-penetration-testing-lab-1-7544969cb3ac "https://medium.com/@ehsahil/basic-penetration-testing-lab-1-7544969cb3ac")[](https://medium.com/@ehsahil/basic-penetration-testing-lab-1-7544969cb3ac)

[**Basic iOS Apps Security Testing lab — 1**  
_Hi Everyone,_medium.com](https://medium.com/@ehsahil/basic-ios-apps-security-testing-lab-1-2bf37c2a7d15 "https://medium.com/@ehsahil/basic-ios-apps-security-testing-lab-1-2bf37c2a7d15")[](https://medium.com/@ehsahil/basic-ios-apps-security-testing-lab-1-2bf37c2a7d15)

[**Basic Android Security Testing lab — 1**  
_Hi Everyone,_medium.com](https://medium.com/@ehsahil/basic-android-security-testing-lab-part-1-a2b87e667533 "https://medium.com/@ehsahil/basic-android-security-testing-lab-part-1-a2b87e667533")[](https://medium.com/@ehsahil/basic-android-security-testing-lab-part-1-a2b87e667533)

**6.3 — Best Security Checklists out there.**

[**SaaS CTO Security Checklist | Sqreen**  
_Learn how to protect your SaaS applications with the SaaS CTO security checklist. Select your startup stage and use…_www.sqreen.com](https://www.sqreen.com/checklists/saas-cto-security-checklist "https://www.sqreen.com/checklists/saas-cto-security-checklist")[](https://www.sqreen.com/checklists/saas-cto-security-checklist)

[**Pentest Best Practices Checklist | Sqreen**  
_Sqreen is a SaaS platform which automatically protects your web applications, in 30 seconds, with no code modification._www.sqreen.com](https://www.sqreen.com/checklists/pentest-checklist "https://www.sqreen.com/checklists/pentest-checklist")[](https://www.sqreen.com/checklists/pentest-checklist)

[**The First Security Engineer's 100-day Checklist | Sqreen**  
_Sqreen is a SaaS platform which automatically protects your web applications, in 30 seconds, with no code modification._www.sqreen.com](https://www.sqreen.com/checklists/security-engineer-checklist "https://www.sqreen.com/checklists/security-engineer-checklist")[](https://www.sqreen.com/checklists/security-engineer-checklist)

[**Devops Security Checklist | Sqreen**  
_Learn how to integrate security into DevOps with the Devops Security Checklist. Protect your app, infra and more._www.sqreen.com](https://www.sqreen.com/checklists/devops-security-checklist "https://www.sqreen.com/checklists/devops-security-checklist")[](https://www.sqreen.com/checklists/devops-security-checklist)

[**DevSecOps Security Checklist | Sqreen**  
_Sqreen is a SaaS platform which automatically protects your web applications, in 30 seconds, with no code modification._www.sqreen.com](https://www.sqreen.com/checklists/devsecops-security-checklist "https://www.sqreen.com/checklists/devsecops-security-checklist")[](https://www.sqreen.com/checklists/devsecops-security-checklist)

[**AWS Security Best Practices**  
_Sqreen is a SaaS platform which automatically protects your web applications, in 30 seconds, with no code modification._www.sqreen.com](https://www.sqreen.com/resources/aws-security "https://www.sqreen.com/resources/aws-security")[](https://www.sqreen.com/resources/aws-security)

**6.4 — Awesome Incident response**

[**meirwah/awesome-incident-response**  
_A curated list of tools for incident response. Contribute to meirwah/awesome-incident-response development by creating…_github.com](https://github.com/meirwah/awesome-incident-response "https://github.com/meirwah/awesome-incident-response")[](https://github.com/meirwah/awesome-incident-response)

**6.5 — Awesome Threat detection and intelligence**

[**0x4D31/awesome-threat-detection**  
_A curated list of awesome threat detection and hunting resources - 0x4D31/awesome-threat-detection_github.com](https://github.com/0x4D31/awesome-threat-detection "https://github.com/0x4D31/awesome-threat-detection")[](https://github.com/0x4D31/awesome-threat-detection)

[**hslatman/awesome-threat-intelligence**  
_A curated list of Awesome Threat Intelligence resources - hslatman/awesome-threat-intelligence_github.com](https://github.com/hslatman/awesome-threat-intelligence "https://github.com/hslatman/awesome-threat-intelligence")[](https://github.com/hslatman/awesome-threat-intelligence)

### ANDDDD…Still, only 1% done……

#### **until next time.**