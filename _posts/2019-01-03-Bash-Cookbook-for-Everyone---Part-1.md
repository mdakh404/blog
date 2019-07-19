---
layout: post
title: Bash Cookbook for Everyone — Part 1
---

**Hi Guys,**

This bash cookbook I created while learning the bash recently. I’ve put a lot of efforts in assembling the useful information and resources. I’ve divided this cookbook into two parts, first, one will be focused on bash and the second one will be on Unix commands and useful one-liners.

### Table of Contents

**Part-1 — **[**Shell Scripting**](https://medium.com/p/9347555ba846#d043)

*   [Pipelines](https://medium.com/p/9347555ba846#07bd)
*   [BASH — Bourne Again Shell](https://medium.com/p/9347555ba846#15a8)
*   compound commands
*   [Running bash scripts](https://medium.com/p/9347555ba846#5a7b)
*   File Permissions

3\. [**Bash scripts.**](https://medium.com/p/9347555ba846#c9e5)

4\. **Part-2**

### Shell scripting.

Shell scripting is a computer programming which contains the series of Unix commands.

A shell is a command-line interpreter and typical operations performed by shell scripts include file manipulation, program execution, and printing text.  
Types of shells.

Shell Startup Process — BASH/SH/ZSH Startup Process.

![Shell Startup — Sh/Bash/zsh | Source — zwischenzugs.com](https://cdn-images-1.medium.com/max/800/1*xgmeKpaKRNBtTLcfnlwL1Q.png)
Shell Startup — Sh/Bash/zsh | Source — zwischenzugs.com

Valid Login shell for my machine —

cat /etc/shells

![](https://cdn-images-1.medium.com/max/800/1*qMG0UX7_Y5zcuwP6OApgrQ.png)

**Type of shell.**

*   /bin/bash — Bourne Again shell
*   /bin/csh — C shell
*   /bin/ksh — Korn Shell
*   /bin/sh — Bourne Shell, The original shell still used in UNIX.
*   /bin/tcsh — TENEX C Shell, a superset of the common C shell.

When the shell is started, it read the configuration files, The most commons are.

*   /etc/profile
*   ~/.bash\_profile
*   ~/.bashrc
*   ~/.bash\_logout — Contains the instructions for logout procedure. (don’t f\*ck with it)

**Usefulness of shell scripting**

*   They remember commands.
*   They allow you to reuse the commands.
*   they let you edit the command.
*   Shells are highly programmable.

[**Upcase : Mastering the Shell Course | Upcase Tutorials** ](https://thoughtbot.com/upcase/mastering-the-shell "https://thoughtbot.com/upcase/mastering-the-shell")[](https://thoughtbot.com/upcase/mastering-the-shell)

#### Pipelines

Pipelines are one or more [**simple commands**](http://wiki.bash-hackers.org/syntax/basicgrammar#simple_commands "syntax:basicgrammar") (separated by the `_|_` symbol connects their input and output),

[**Simple, Fast, Easy Parallelism in Shell Pipelines** ](https://catern.com/posts/pipes.html "https://catern.com/posts/pipes.html")[](https://catern.com/posts/pipes.html)

**ls -l /usr/bin | less | sort | uniq | wc -l**

![](https://cdn-images-1.medium.com/max/800/1*mc1baaDaEa1SkrWa8w_HYQ.png)

### Bash — Bourne Again Shell

Bash is a standard shell, which is intuitive and flexible. In Linux and MacOS, Bash is a standard shell for common users. Bash is also a superset of the Bourne shell.

The primary purpose of bash is to allow you to interact with the computers’ OS so that you can accomplish whatever you need to do. Bash is just a language to execute the command.

**Bash Built-in commands**

**alias**, **bind**, **builtin**, **command**, **declare**, **echo**, **enable**, **help**, **let**, **local**, **logout**, **printf**, **read**, **shopt**, **type**, **typeset**, **ulimit** and **unalias**.

The main use of the bash is to allow you to interact with the computers OS, so that you can accomplish, whatever you need to do.

bash is a simple language, which allows you to execute some commands in a programmable way.

bash --version

You can update the bash using the following command.

**apt-get update && apt-get install bash bash3 bash-builtins bash-doc bash3-doc**

### Compound commands —

*   Grouping Commands in a subshell
*   Arithmetic Evaluation
*   The conditional Expression
*   The classic for-loop
*   The C-style for-loop
*   User Selection
*   The Case statement
*   The If-clause
*   The while loop
*   The until loop

Compound commands have the following characteristics:

*   They begin and end with a specific keyword or operator ( eg **for** … **done**)
*   They can be redirected as the whole.

> **Grouping Commands in a subshell (<list>) **— The list is executed in a separate shell — a subprocess.

(cd opt/tools/VHostScan/; ls)

![](https://cdn-images-1.medium.com/max/800/1*-zwbWHl0J7tNBqhrFuD9XA.png)

> **Grouping Commands {<list>} **— The list command is simply executed in the current shell environment, the command must be terminated with newline or semicolon.

{ cd opt/tools/VHostScan/; ls; }

![](https://cdn-images-1.medium.com/max/800/1*lVYr9ac7jdHcefmDfvG36Q.png)

> **Arithmetic Evaluation (( <Expression> )) **— This command evalauates the arithmetic expression.

In arithmetic evaluation **0** is FALSE and **1** is TRUE

In the above script, if you type 1 \`**Your choice is TRUE**\` will return and if you type 0 \`**Your choice is FALSE**\`

![](https://cdn-images-1.medium.com/max/800/1*4kNXtq9Roevhq4S8fW1U3w.png)

> **The conditional Expression \[\[<expression>\]\] **— The conditional expression is meant for use as a conditional command like.

```
<expression1> && <expression2>

<expression1> || <expression2>

<expression1> == <expression2>

<expression1> = <expression2>

<expression1> != <expression2>

```

Example script —

![](https://cdn-images-1.medium.com/max/800/1*iE6M6sPgrLVV9KoBlLyoBA.png)

> **The classic for-loop** —

for <name> in <words> ; do <list>; done

Getting Ip using dig and doing a whois on IP is taken from Dig.

**for ip in \`dig** [**www.google.com**](http://www.google.com) **+short\`; do whois $ip; done**

![](https://cdn-images-1.medium.com/max/800/1*NvDH_ftxRCVzBvzulEy6MA.png)

**for IP in \`cat company\_ip.txt\`; do echo "$IP =>\`dig -x $IP +short\`";done**

for IP in \`cat company\_ip.txt\`; do echo "$IP =>\`Any command you want to run\`";done

for subdomain in \`cat test.com\`; do echo "Working on $subdomain =>\`ds $subdomain\`";done

![](https://cdn-images-1.medium.com/max/800/1*yYhF8YdMgN9rTFHFickKvQ.png)

Creating and deleting multiple files.

**for x in \`seq 1 5\`; do touch ehsahil\_file\_${x}.txt; done** //creating **  
for x in \`seq 1 5\`; do rm  ehsahil\_file\_${x}.txt; done** //deleting

**for files in /media/\* do echo $files done**

![](https://cdn-images-1.medium.com/max/800/1*jbaf_KAEJotxCAvq0rOovA.png)

Extracting multiple files in one command.

**for i in $(ls \*.tar.gz); do tar zxvf $i; done**

> **The C-style for-loop** —

```

for ((<Expr1>;<expr2>;<expr3>;)); do <list> ;done

Example: —

for ((x=1; x<=3; x++))  
{  
    echo $x  
}

Simple Counter:

for ((x = 0 ; x <= 100 ; x++)); do  
  echo "Counter: $x"  
done
```

![](https://cdn-images-1.medium.com/max/800/1*GfcKGLgbZMkxrr7nN7bp3g.png)

Stepping counter

for ((x = 0 ; x <= 100 ; x += 10)); do  
  echo "Counter: $x"  
done

![](https://cdn-images-1.medium.com/max/800/1*X7YDWrzoyIouDZQibR-HUg.png)

> **User Selection** —

```

select <NAME> in <WORDS> ; do <LIST> ; done

select x in 1 2 3  
{  
  echo $x  
}
```

![](https://cdn-images-1.medium.com/max/800/1*zbo83vf3jhmvgOSA95s-RA.png)

> **The Case statement **— The case-statement can execute commands based on a pattern matching decision

![](https://cdn-images-1.medium.com/max/800/1*Hun2UlsX2RQwfIHW6wFWLg.png)

> **The If-clause** — The `_if_`\-clause can control the script's flow (what's executed) by looking at the exit codes of other commands.

![](https://cdn-images-1.medium.com/max/800/1*zfU_LshDb9aE30Bd4HhnTg.png)

> **The while loop **— The while-loop is relatively simple in what it does: it executes the [command list](http://wiki.bash-hackers.org/syntax/basicgrammar#lists "syntax:basicgrammar") `_<LIST1>_` and if the exit code of it was 0 (TRUE) it executes `_<LIST2>_`. This happens again and again until `_<LIST1>_` returns FALSE.

while <LIST1> ; do  
  <LIST2>  
done

> **The until loop **— The until-loop is relatively simple in what it does: it executes the [command list](http://wiki.bash-hackers.org/syntax/basicgrammar#lists "syntax:basicgrammar") `_<LIST1>_` and if the exit code of it was **not** 0 (FALSE) it executes `_<LIST2>_`. This happens again and again until `_<LIST1>_` returns TRUE.

until <LIST1> ; do  
  <LIST2>  
done

### Running Bash Scripts

The script should have execute permission for the correct owner for running. we can change the permission using `chmod`

chmod u+x script.sh

Defining which shell to run,

#!/bin/bash

We need to give the proper permission to the script before running it.

**Understanding permissions within Unix.**

[**Creating a bash completion script** ](https://iridakos.com/tutorials/2018/03/01/bash-programmable-completion-tutorial "https://iridakos.com/tutorials/2018/03/01/bash-programmable-completion-tutorial")[](https://iridakos.com/tutorials/2018/03/01/bash-programmable-completion-tutorial)

[**Ten Things I Wish I’d Known About bash** ](https://zwischenzugs.com/2018/01/06/ten-things-i-wish-id-known-about-bash/ "https://zwischenzugs.com/2018/01/06/ten-things-i-wish-id-known-about-bash/")[](https://zwischenzugs.com/2018/01/06/ten-things-i-wish-id-known-about-bash/)

**bash is all you need.**

#### Bash script

Convert domain list to resolved IP address list.

![](https://cdn-images-1.medium.com/max/800/1*fhI3M3x-OBLaO3ReW_7XVg.png)

Checking for zone transfer.

```
#!/bin/bash
```

```
for
```

```
do
```

```
done
```

Give proper permission.

chmod +x zonetransfer.sh

![](https://cdn-images-1.medium.com/max/800/1*dQ603Lz-0VacIbcmeMRRGw.png)

**Reverse lookup for each IP in a subnet.**

```

#!/bin/bash  
   
i="1"  
   
echo "Please enter first 3 octets. e.g 192.168.1"  
read subnet  
        while \[ $i -le 254 \]; do  
        host -l "$subnet"."$i"  
        i=$(( $i + 1))  
        done
```

![](https://cdn-images-1.medium.com/max/800/1*JfdIQt35i2pPmpZ7ZzLhAw.png)

**Tips?**

The more you practice bash and use it for day to day work, the more you will become good at it.

#### Nothing more to see here.

#### Yea !! — Part-2

[**Bash Cookbook for Everyone — Part 2**  
_Part-1_medium.com](https://medium.com/ehsahil/bash-cookbook-for-everyone-part-2-b70d40610025 "https://medium.com/ehsahil/bash-cookbook-for-everyone-part-2-b70d40610025")[](https://medium.com/ehsahil/bash-cookbook-for-everyone-part-2-b70d40610025)

Good read, If interested : —
