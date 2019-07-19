---
layout: post
title: Bash Cookbook for Everyone — Part 2
---

#### [Part-1] (https://ehsahil.com/Bash-Cookbook-for-Everyone-Part-1)

**Part-2 — Learn Core Unix Commands.**

*   [**Working with commands**](https://medium.com/p/b70d40610025#2e36)— type, which, help, man, info, whatis, alias
*   [**Exploring the file system commands**](https://medium.com/p/b70d40610025#943f)\- ls, pwd, file, more, less
*   [**Manipulating files and directories commands** ](https://medium.com/p/b70d40610025#599f)— cp, mv, mkdir, rm
*   [**Redirection Commands **](https://medium.com/p/b70d40610025#431f)— cat, sort, uniq, grep, wc, head, tail
*   [**Permissions Commands**](https://medium.com/p/b70d40610025#cd93)— id, cdmod, su, sudo, passwd
*   [**Processes Commands** ](https://medium.com/p/b70d40610025#3969)— ps, top, bg, fg, kill, killall, shutdown,
*   [**Environment commands** ](https://medium.com/p/b70d40610025#f0e2)— printenv, set, vim
*   [**Networking Commands **](https://medium.com/p/b70d40610025#f0c0)— ping, traceroute, dig, ip, netstat, wget, curl, ifconfig etc
*   [**searching of files commands**](https://medium.com/p/b70d40610025#2f67)\- locate, find,
*   [**text processing commands **](https://medium.com/p/b70d40610025#a68e)— cut, sed, awk, parallel
*   [**more commands**](https://medium.com/p/b70d40610025#4c9b) — clear, history,

3\. [**One-liners**](https://medium.com/p/b70d40610025#37fe)

4\. [**References**](https://medium.com/p/b70d40610025#387a)

### Learn Basic Unix Commands.

#### Working with commands

> **type** — Display’s commands type

```
man type //Type Command manual page

type commands
```

> **which** — Display which program will be executed.

```
man which //Which command manual p  
which ls
```

> **help** — Get help

```
help

help cd

mkdir --help
```

> **man** — Display manual pages

> **info** — Display commands info entry

```
man info
```

**info coreutils**

> **whatis** — very brief description of the command.

```
man whatis

whatis ls

```

> **alias **— Create an alias for a command.

```
alias l.='ls -d .\* --color=tty'  
alias ll='ls -l --color=tty'  
alias ls='ls --color=tty'  
unalias which //removing alias
```

#### Exploring the file system Commands.

> **ls** — list directory contents

```
man ls

Useful **ls** Commands

ls -lt --reversels

ls -li

ls > list.txt

ls -l

LC\_ALL=C ls

ls -l "some\_file"
```

[**exa modern replacement for ls** ](https://the.exa.website "https://the.exa.website")[](https://the.exa.website)

> **lsof** — list open files

> **pwd** — Return working directory name.

```
man pwd
```

> **file** — Determine file types

```
man file
```

file filename

> **more** — file perusal filter for crt viewing

```
man more
```

> **less** — View file content

#### Manipulating files and directories Commands.

> **cp** — copy files and directories.

[**Clément Chastagnol ~ Moving efficiently in the CLI** ](https://clementc.github.io/blog/2018/01/25/moving_cli/ "https://clementc.github.io/blog/2018/01/25/moving_cli/")[](https://clementc.github.io/blog/2018/01/25/moving_cli/)

```
man cp

cp file.html /usr/local/bin
```

> **mv** — move and rename files and directories.

```
man mv

mv file.html /usr/localbin //moving files

mv file.html file2.html //renaming files.

```

> **mkdir** — create directories

```
man mkdir

mkdir somedirectory  
mkdir dir1 dir2 dir3

```

> **rm** — remove files and directories

**Caution**: Be careful with rm

```

man rm

rm file.txt

rm -i //interective - if this option is not defined, rm will delete files silently.

rm -r //recursive recursively delete directories.

rm -f //force delete.

rm -v //Display informative messages.

rm -rf file1 dir1 //if nither file1 or dir1 exists rm will countinue silently.
```

#### Redirection Commands

Redirection makes it possible to control where the output of command goes to, and where the input of command comes from.

```
stdin - standard input stream (eg- keyboard)  
stdout - standard output stream (eg- monitor)  
stderr - standard error output.

```

\# Below cat-command will execute and redirect its error to (stderr) #to the bit bucket

cat file.txt 2>/dev/null

\# below echo-command will execute and redirect its normal outout (stdout).

echo "there was an error" 1>&2

> **cat** — concatenate files

[**The Source History of Cat** ](https://twobithistory.org/2018/11/12/cat.html "https://twobithistory.org/2018/11/12/cat.html")[](https://twobithistory.org/2018/11/12/cat.html)

man cat #Manual page

```
cat 1.txt 2.txt > new.txt  
cat >new.txt 1.txt 2.txt  
\>new.txt cat 1.txt 2.txt
```
> **sort** — Sort or merge records (lines) of text and binary files.

```
man sort

cat -n file.txt // file cat with no of lines.

cat company\_ip | sort -t . -k 1,1n -k 2,2n -k 3,3n -k 4,4n ipaddr.list
```

![](https://cdn-images-1.medium.com/max/800/1*49EwA0uKsvZACjic5_DvCg.png)

Wow, that’s ugly. Here it is in the old format:

```
cat company\_ip | sort -t. +0n -1 +1n -2 +2n -3 +3n -
```

> **uniq** — report or omit repeated lines

man uniq

> **grep** — print matching a pattern

[**find, grep, sed, and awk.**  ](https://wilsonericn.wordpress.com/2011/08/25/find-grep-sed-and-awk/ "https://wilsonericn.wordpress.com/2011/08/25/find-grep-sed-and-awk/")[](https://wilsonericn.wordpress.com/2011/08/25/find-grep-sed-and-awk/)

```
man grep

grep root /etc/passwd

grep -n root /etc/passwd

grep -v bash /etc/passwd | grep -v nologin

grep -c false /etc/passwd

grep -i ps ~/.bash\* | grep -v history
```

> **wc** — print newline, word, and byte count for each file

man wc

> **head** — output first part of the file

> **tail** — output last part of the file

#### Permissions Commands

> **id** — Display user identity

man id

> **chmod** — change a file’s mode

```
man chmod

chmod u+x script.sh

chmod +x script.sh
```

> **su** — Substitute user identity or run the shell as another user


```
man su
```

> **sudo** — Execute a shell as another user

```
man sudo
```

> **passwd** — Modify a user’s password

```
man passwd
```

#### Processes Commands

> **ps** — Report current processes

```
ps x

ps aux

ps -ef

**ps -ef | grep _stuck\_process_**

**kill -9 _5607_**
```

When a process starts up several instances, **killall** might be easier. It takes the same option as the **kill** command but applies on all instances of a given process.

> **top** — Display task

> **bg** — put a job in the background

> **fg** — put a job in the foreground

> **kill** — send a signal to a process

> **killall** — kill processes by name

### Environment commands

> **printenv** — print all or part of the environment

Env and printenv commands used to display the environment variable.

printenv or env

man printenv

printenv | less

printenv USER

> **set** — set shell options

```
set | less

set -o // display all shell options
```

> **Vim — **Vi IMproved. a programmer’s text editor.

```
man vim
```

**Benefits of using vim**

vim is always available & vim is lightweight and fast

```
vi filname-txt

Enter "i" to edit

:q to exit and save

:q! to force exit and save

o - The line below the current line.

O - The line above the current line.
```

[**The Vim Learning Curve is a Myth** ](https://robots.thoughtbot.com/the-vim-learning-curve-is-a-myth "https://robots.thoughtbot.com/the-vim-learning-curve-is-a-myth")[](https://robots.thoughtbot.com/the-vim-learning-curve-is-a-myth)

[**Upcase : Onramp to Vim | Online Tutorial by thoughtbot** ](https://thoughtbot.com/upcase/onramp-to-vim "https://thoughtbot.com/upcase/onramp-to-vim")[](https://thoughtbot.com/upcase/onramp-to-vim)

[**Vim for humans** ](https://vimebook.com/en "https://vimebook.com/en")[](https://vimebook.com/en)

if interested. good read

[**Where Vim Came From**  ](https://twobithistory.org/2018/08/05/where-vim-came-from.html "https://twobithistory.org/2018/08/05/where-vim-came-from.html")[](https://twobithistory.org/2018/08/05/where-vim-came-from.html)

#### Networking Commands —

Important networking files within the local machine.

```

*   /etc/hosts — Name to the Ip address
*   /etc/networks — Network name to the IP address
*   /etc/protocol — Protocol name to the Protocol number.
*   /etc/services — TCP/UDP names to the port number.

```

> **ping** — Send an ICMP ECHO\_REQUEST to network hosts

```
man ping
```

> **traceroute** — Print the route packets trace to a network host, Route taken by packets to a specific Ip Address.

```
man traceroute`
```

> **Dig** — DNS lookuup Utility

> **netstat** — Show network status, what connection is active between the local machine and another network machine.

```
man netstat

netstat -ie

netstat -r
```

> **netcat** — Netcat is a simple Unix utility which reads and writes data across network connections,

> **Iptable — **administration tool for IPv4/IPv6 packet filtering and NAT

> **IP** — IP is the transport layer protocol used by the Internet protocol family.

> **SSH** — Secure Shell

[**22 SSH Examples, Practical Tips & Tunnels | HackerTarget.com**  ](https://hackertarget.com/ssh-examples-tunnels/ "https://hackertarget.com/ssh-examples-tunnels/")[](https://hackertarget.com/ssh-examples-tunnels/)

> **wget** — The non-interactive network downloader.

```
man wget
```

> **curl — **tranfer a URL

```
man curl
```

Getting subdomains from curl using certspotter.com

```
**curl -s** [**https://certspotter.com/api/v0/certs\\?domain\\=deliveroo.co.uk**](https://certspotter.com/api/v0/certs%5C?domain%5C=deliveroo.co.uk) **| jq '.\[\].dns\_names\[\]' | sed 's/\\\*\\.//g' | tr -d "\\"" | sort -u**

```

![](https://cdn-images-1.medium.com/max/800/1*8a17hAK2K_IgHkwizctFwg.png)

Cool `bash_profile` by [Behrouz Sadeghipour](https://medium.com/u/9a72584d6865)

[**nahamsec/recon\_profile**  
_Contribute to nahamsec/recon\_profile development by creating an account on GitHub._github.com](https://github.com/nahamsec/recon_profile "https://github.com/nahamsec/recon_profile")[](https://github.com/nahamsec/recon_profile)

you can add the recon\_profile in `bash_profile` present in the root directory.

![](https://cdn-images-1.medium.com/max/800/1*kl4roPKWc6e99AgUJdSQqw.png)

you can also customize it according to your need.

#### Searching for files commands —

> **locate** — locate the file by name

```
man locate

locate bin/zip  
locate zip | grep bin
```

> **find** — search for filesman find

[**Find is a beautiful tool**  ](https://www.eriwen.com/productivity/find-is-a-beautiful-tool/ "https://www.eriwen.com/productivity/find-is-a-beautiful-tool/")[](https://www.eriwen.com/productivity/find-is-a-beautiful-tool/)

```
find ~  
find ~ | wc -l  
find ~ -type d | wc -l

find ~ -type f | wc -l  
find ~ -type f -name "\*.JPG" -size +1M | wc -l 840
```

#### text processing commands,

**cut — **cut out a selected portion of each line of a file.

```
man cut
```

> **sed — **Stream Editor is used to perform basic transformation on read text from a file or a pipe. sed is also sometimes known as bash editor.

[http://www.pement.org/sed/sed1line.txt](http://www.pement.org/sed/sed1line.txt)

> **awk — **pattern-directed scanning and processing language

AWK: Effective AWK Programming: A User’s Guide for GNU Awk

the basic function of awk is to search files for lines or other text unit text containing one or more pattern. when a line matches one of the patterns, special action is performed on that line.

**awk 'EXPRESSION { PROGRAM }' file(s)**

The variables $1, $2, $3, …, $N hold the values of the first, second, third until the last field of an input line. The variable $0 (zero) holds the value of the entire line.

```
man awk
```

```
**ls -l | awk _'{ print $5 $9 }'_**
```


```
**history | awk 'BEGIN {FS="\[ \\t\]+|\\\\|"} {print $3}' | sort | uniq -c | sort -nr | head**
```

Remove duplicate lines: **awk '!a\[$0\]++'**

> **Parallel —**

We can use the parallel command to resolve the multiple javascript URLs present in a text file.

we can use [TomNomNom](https://twitter.com/TomNomNom) way back URL to get javascript files URLs.

waybackurls deliveroo.com | grep ".js" > deliveroo-js.txt

cat **deliveroo-js.txt** | parallel -j50 -q curl -w 'Status:%{http\_code}\\t Size:%{size\_download}\\t %{url\_effective}\\n' -o /dev/null -sk

![Thanks to Bharat from Appsecco.](https://cdn-images-1.medium.com/max/800/1*xrAvDUn9YL1MsLSzfsUe3Q.png)
Thanks to Bharat from Appsecco.

#### More commands

> **clear** — clear the terminal screen.

```
man clear
```

> **History** — Display the content of the history list

```
histroy | less
```

**!88** - bash will expand “!88” into the contents of the 88th line in the history list

**!!** - Repeat the last command

Display most used commands

**history | awk 'BEGIN {FS="\[ \\t\]+|\\\\|"} {print $3}' | sort | uniq -c | sort -nr | head**

> **Git** — the stupid content tracker

Git is a fast, scalable, distributed revision control system with an unusually rich command set that provides both

high-level operations and full access to internals.

[**Upcase : Mastering Git - Online Tutorial by thoughtbot** ](https://thoughtbot.com/upcase/mastering-git "https://thoughtbot.com/upcase/mastering-git")[](https://thoughtbot.com/upcase/mastering-git)

[**Learn Git Branching**  ](https://learngitbranching.js.org/ "https://learngitbranching.js.org/")[](https://learngitbranching.js.org/)

### One-Liners

**ASN** — An autonomous system number (ASN) is a unique number assigned to an autonomous system (AS) by the Internet Assigned Numbers Authority (IANA).

ASN Example : - AS63086

[https://iptoasn.com/](https://iptoasn.com/)

**CIDR**(Classless Inter-Domain Routing or supernetting ) — is a way to allow more flexible allocation of Internet Protocol (IP) addresses than was possible with the original system of IP address classes.

A CIDR network address looks like this under IPv4:

192.30.250.00/18

[https://www.cidr-report.org/as2.0/autnums.html](https://www.cidr-report.org/as2.0/autnums.html)

Get CIDR from ASN numbers.

```
whois -h whois.radb.net -- '-i origin AS63086' | grep -Eo "(\[0-9.\]+){4}/\[0-9\]+" | head
```

![](https://cdn-images-1.medium.com/max/800/1*xsXAqYujMjw00zbMCgIc6w.png)

**CIDR to IP addresses using nmap**

```
nmap -sL 104.36.192.0/24 | grep "Nmap scan report" | awk '{print $NF}'
```

![](https://cdn-images-1.medium.com/max/800/1*R7cLN7YUTg-zIeGbhaK8wg.png)

Finding Up hosts using NMAP.

```
nmap -sP 104.36.192.0/21 -oG uber-ips.txt
```

![](https://cdn-images-1.medium.com/max/800/1*s05oTMn8R4jrG22fSAH-rw.png)

**Grep fro UP hosts only.**

```
cat uber-ips.txt | grep Up | cut -d" " -f2
```

![](https://cdn-images-1.medium.com/max/800/1*Gqu9dN4ItV19cCQmZkDThQ.png)

Saving UP hosts as `uber-up-hosts.txt`

Running masscan on `uber-up-hosts.txt`

masscan -iL uber-up-hosts.txt -p80,443,8080,8000,9000,8888,9999 --rate 10000 --open

![](https://cdn-images-1.medium.com/max/800/1*3EYUoRq2F00GU5snBI5cFA.png)

**Find your IP address using the command line:**

```
**/sbin/ifconfig -a | awk '/(cast)/ { print $2 }' | cut -d':' -f2 | head -1**
```

**Pulling IP address from a file.**

```
**grep -E -o '\[0-9\]{1,3}\\.\[0-9\]{1,3}\\.\[0-9\]{1,3}\\.\[0-9\]{1,3}'**
```

**Subdomains from hacker target**

```
**curl -s** [**https://api.hackertarget.com/hostsearch/?q=deliveroo.com**](https://api.hackertarget.com/hostsearch/?q=deliveroo.com) **| cut -d',' -f1 | sort -u**
```

![](https://cdn-images-1.medium.com/max/800/1*mat02ZzKufaMhExcP1bn5A.png)

**Subdomains from Threatcrowd**

```
curl -s https://www.threatcrowd.org/searchApi/v2/domain/report/?domain=deliveroo.com  | jq -r '.subdomains | .\[\]' | sort -u
```

![](https://cdn-images-1.medium.com/max/800/1*4UMTp3lu1-2oLuuIEKFDpg.png)

**Subdomains from Certspotter**

```
curl -s [https://certspotter.com/api/v0/certs\\?domain\\=deliveroo.co.uk](https://certspotter.com/api/v0/certs%5C?domain%5C=deliveroo.co.uk) | jq '.\[\].dns\_names\[\]' | sed 's/\\\*\\.//g' | tr -d "\\"" | sort -u
```

![](https://cdn-images-1.medium.com/max/800/1*VsoaF-4Ibdr0C5AcgbwWzg.png)

**Subdomain from crt.sh**

```
curl -s https://crt.sh/?q=%.hackerone.com | sed '/crt/d' | sed 's/<\\/\\?\[^>\]\\+>//g' | tr -d ' ' | sed 's/  \*/ /g' | sed 's/\\\*\\.//g' | sed 's/\\%\\.//g' | sed -e '1,2d' | sort -u | uniq | grep hackerone | sed '/IdentityLIKE/d'
```

![](https://cdn-images-1.medium.com/max/800/1*JIXC14sMidgEUc07lmwhQA.png)

**subdomains from Archive.**

```
curl -s "http://web.archive.org/cdx/search/cdx?url=\*.hackerone.com/\*&output=text&fl=original&collapse=urlkey" |sort| sed -e 's\_https\*://\_\_' -e "s/\\/.\*//" -e 's/:.\*//' -e 's/^www\\.//' | sort -u
```

![](https://cdn-images-1.medium.com/max/800/1*JIXC14sMidgEUc07lmwhQA.png)

```
cat deliveroo-domains.txt | filter-resolved > deliveroo-domains-resolved.txt
```

![](https://cdn-images-1.medium.com/max/800/1*K4MvBTRRhtNIo7cr1htzsg.png)

fetch titles of the subdomains from a list using `httprobe`and `get-title`

```
cat deliveroo-domains.txt | httprobe | get-title
```

![](https://cdn-images-1.medium.com/max/800/1*jZncrFuL90S983ZzDQysHw.png)

**Fetching interesting URL from** `**waybackmachine**`

```
echo hackerone.com | waybackurls | tee test.txt | urinteresting
```

![](https://cdn-images-1.medium.com/max/800/1*8lrJOJrjjNsmmf0DB5twaw.png)

Subdomain from SSL certificates.

```
true | openssl s\_client -connect hackerone.com:443 2> /dev/null | openssl x509 -noout -text 2> /dev/null | grep DNS: | sed 's/ DNS://g' | sed 's/ //g' | sed 's/,/\\'$'\\n/g'  
```
  

![](https://cdn-images-1.medium.com/max/800/1*4wh2_kSuA3P8kQmuZfUNrQ.png)

[**bash,pentesting one-liners and stuff**  ](https://bloggins-sec.blogspot.com/2013/01/bashpentesting-one-liners-and-stuff.html "https://bloggins-sec.blogspot.com/2013/01/bashpentesting-one-liners-and-stuff.html")[](https://bloggins-sec.blogspot.com/2013/01/bashpentesting-one-liners-and-stuff.html)

[**Command Line for the 21. Century: The Low Hanging Fruit**  ](https://ileriseviye.wordpress.com/2018/10/30/command-line-for-the-21-century-the-low-hanging-fruit/ "https://ileriseviye.wordpress.com/2018/10/30/command-line-for-the-21-century-the-low-hanging-fruit/")[](https://ileriseviye.wordpress.com/2018/10/30/command-line-for-the-21-century-the-low-hanging-fruit/)

[**10 Linux Commands That Will Save Your Time — Azer Koçulu’s Journal** ](https://azer.bike/journal/10-linux-commands-that-will-save-your-time/ "https://azer.bike/journal/10-linux-commands-that-will-save-your-time/")[](https://azer.bike/journal/10-linux-commands-that-will-save-your-time/)

#### Command line basic shortcuts

```
ctrl + a - move cursor to the begining of the line  
ctrl + e - move cursor to the end of the line.   
Alt+f - move one word forward  
Alt+b Move cursor one work backword  
ctrl+l- clear the clean (clear command alternative)
```

[**Become a Command Line Ninja With These Time-Saving Shortcuts** ](https://lifehacker.com/5743814/become-a-command-line-ninja-with-these-time-saving-shortcuts "https://lifehacker.com/5743814/become-a-command-line-ninja-with-these-time-saving-shortcuts")[](https://lifehacker.com/5743814/become-a-command-line-ninja-with-these-time-saving-shortcuts)

#### Personal Aliases —

these are the only tip of the iceberg,

more one-liners?

practice and make one-liners according to your need.

### References

Thanks to all of the following peoples for creating awesome content.

**Bash Cookbook** by _Carl Albing, JP Vossen, and Cameron Newham_

**The Linux Command Line** by  William Shott

**Penetration Testing with the Bash Shell** by Keith Makan

[**Bash tips for everyday at the command line**  ](https://opensource.com/article/18/5/bash-tricks "https://opensource.com/article/18/5/bash-tricks")[](https://opensource.com/article/18/5/bash-tricks)

[**We all ❤ Terminals. — Terminals Are Sexy** ](https://terminalsare.sexy/ "https://terminalsare.sexy/")[](https://terminalsare.sexy/)

[**Bash Scripting 101 for Pen Testers Hack3rcon 3 (Hacking Illustrated Series InfoSec Tutorial Videos)** ](http://www.irongeek.com/i.php?page=videos/hack3rcon3/09-bash-scripting-101-for-pen-testers-lee-baird "http://www.irongeek.com/i.php?page=videos/hack3rcon3/09-bash-scripting-101-for-pen-testers-lee-baird")[](http://www.irongeek.com/i.php?page=videos/hack3rcon3/09-bash-scripting-101-for-pen-testers-lee-baird)

[**Shell startup scripts — flowblok’s blog**  ](https://blog.flowblok.id.au/2013-02/shell-startup-scripts.html "https://blog.flowblok.id.au/2013-02/shell-startup-scripts.html")[](https://blog.flowblok.id.au/2013-02/shell-startup-scripts.html)

[**Unix tool tip (@UnixToolTip) | Twitter**  ](https://twitter.com/UnixToolTip "https://twitter.com/UnixToolTip")[](https://twitter.com/UnixToolTip)

[**Penetration Testing with the Bash shell** ](https://www.amazon.in/Penetration-Testing-shell-Keith-Makan/dp/1849695105 "https://www.amazon.in/Penetration-Testing-shell-Keith-Makan/dp/1849695105")[](https://www.amazon.in/Penetration-Testing-shell-Keith-Makan/dp/1849695105)

[**Bash-it/bash-it**  ](https://github.com/Bash-it/bash-it "https://github.com/Bash-it/bash-it")[](https://github.com/Bash-it/bash-it)

[**The Bash Hackers Wiki \[Bash Hackers Wiki\]**  ](http://wiki.bash-hackers.org/ "http://wiki.bash-hackers.org/")[](http://wiki.bash-hackers.org/)

[**Advanced Bash-Scripting Guide**  ](http://tldp.org/LDP/abs/html/ "http://tldp.org/LDP/abs/html/")[](http://tldp.org/LDP/abs/html/)

[ **Bash Guide for Beginners** ] (http://tldp.org/LDP/Bash-Beginners-Guide/html/ "http://tldp.org/LDP/Bash-Beginners-Guide/html/")[](http://tldp.org/LDP/Bash-Beginners-Guide/html/)

[**uno: a uniq like CLI tool for log data - Unomaly**  ](https://unomaly.com/blog/its-in-the-anomalies/ "https://unomaly.com/blog/its-in-the-anomalies/")[](https://unomaly.com/blog/its-in-the-anomalies/)

[**Learn Bash the Hard Way**  ](https://leanpub.com/learnbashthehardway "https://leanpub.com/learnbashthehardway")[](https://leanpub.com/learnbashthehardway)

[**zwischenzugs**  ](https://zwischenzugs.com "https://zwischenzugs.com")[](https://zwischenzugs.com)

[**offensive Infosec Blog**  ](https://offensiveinfosec.wordpress.com/ "https://offensiveinfosec.wordpress.com/")[](https://offensiveinfosec.wordpress.com/)



#### Until Next Time!
