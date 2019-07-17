---
layout: post
title: Basic iOS Apps Security Testing lab — 1
---

Hi Everyone,
This is a continuous blog post for my — Basic security testing labs setup series.
If you have not read those, I’ve embedded the link below.

* [**Basic Penetration testing lab — 1** ](https://medium.com/ehsahil/basic-penetration-testing-lab-1-7544969cb3ac "https://medium.com/ehsahil/basic-penetration-testing-lab-1-7544969cb3ac")[](https://medium.com/ehsahil/basic-penetration-testing-lab-1-7544969cb3ac)

* [**Basic Android Security Testing lab — Part-1**](https://medium.com/ehsahil/basic-android-security-testing-lab-part-1-a2b87e667533 "https://medium.com/ehsahil/basic-android-security-testing-lab-part-1-a2b87e667533")[](https://medium.com/ehsahil/basic-android-security-testing-lab-part-1-a2b87e667533)

I have collected the resources from many blog posts and included the updated part only. So, That I can use them whenever I am in need. Everyone else also can take reference from it.

When I was setting up the lab, I’ve read many articles but most of them are older and wrote by considering old iOS versions. So, In this post, I tried to add the latest tools and utilities available and tried to include only useful ones.

I am writing this blog post using the following hardware.

* **iPhone 6 — iOS 11.2.6**

* **MacBook Pro — 10.13.6**

#### Preface.

1.  Disclaimer.
2.  Jailbreaking.
3.  Installing Tools and components on IOS device.
4.  Installing iOS Security Tools on MacOS
5.  External Tools/Apps Installation for iOS devices.
6.  Credits and References

### **Disclaimer**

This blog post is meant only for educational purposes and security research.

**jailbreaking —**

Jailbreaking will void the warranty of your device, you might lose all the data from the device, so be smart and please back up your data.

The jailbreaking method totally depends upon the iOS version, Please search online jailbreak for your version and responsibly jailbreak your device.

**Using tools —**

You should also be careful about the tools you are installing from Cydia or from outside. I will not responsible for anything unusable happened after using the following listed tools. BE SMART and analyze the tool before installing or using.

I recommend using the testing virtual machine to set up the lab and testing iOS device.

### JailBreaking —

Jailbreaking is generally are of two types. Jailbreaking totally depends upon the iOS version your device is using.

**Tethered** — A tethered jailbreak requires the iOS to be connected to a computer when turned. If the iPhone is not connected to a computer and booted with special software the device will not enter the jailbroken state.

[https://www.iphonefaq.org/archives/971144](https://www.iphonefaq.org/archives/971144)

**Un-Tethered** — untethered jailbreaks do not require the computer. Everything required to enter the jailbroken state is contained on the iPhone.

I have used this guide to jailbreak my device.

**Jailbreaking iPhone 6 with iOS 11.2.6**

Checking your iOS version

**Settings → General → About**

![](https://cdn-images-1.medium.com/max/800/1*kEFz24wItGCv1-XZ-wQpPQ.png)

I’ve used [https://next.tweakboxapp.com](https://tweakboxapp.com) to download the **Electra 11.3.1** app.

![](https://cdn-images-1.medium.com/max/800/1*-5kHlfCEiDWMzDIH_myTvA.png)

After downloading the app from the tweak box you should see the Electra app in your apps.

![](https://cdn-images-1.medium.com/max/800/1*2sBjQtHEVJLyrHcUEnZnmQ.png)

Open the App and “Enable Jailbreak”. your device will turn off and On multiple times.

![](https://cdn-images-1.medium.com/max/800/1*SWVcOsz1PY0DVSyoeEHU5g.png)

After successful execution, you will see the Cydia in your apps.You might also require to repeat the process multiple times, to get the cydia installed.

![](https://cdn-images-1.medium.com/max/800/1*xcJEwVz7MwcnhLg6PBIwQg.png)

Note — If you turn off your device, you need to enable the jailbreak again.

Cydia home page.

![](https://cdn-images-1.medium.com/max/800/1*oRBTeUcLBwkl8r9msrG-Xg.png)

### Installing Tools and components on IOS device.

*   **BigBoss Recommended Tools.**

This repo on Cydia contains most of the tools required for ios app security testing but due to some problem, I wasn’t able to install tools using it.

So, what I did, I manually downloading the useful tools only, I tried to add the basic information about the tools you should install. So, you have an idea about the tools you are installing.

#### **Downloading tools from Cydia — iOS 11.2.6**

1.  **Network Commands —** This will Install — arp, ifconfig, route and traceroute.

*   **arp** — Arp manipulates or displays the kernel’s IPv4 network neighbour cache. it can add entries to the table, delete one, or display the current content. ARP stands for Address Resolution Protocol, Which is used to find the address of a network neighbour for a given IPv4 address.

[https://www.computerhope.com/unix/arp.htm](https://www.computerhope.com/unix/arp.htm)

*   **ifconfig** — Ifconfig is used to configure or view the configuration of, a network interface.

[https://www.computerhope.com/unix/uifconfi.htm](https://www.computerhope.com/unix/uifconfi.htm)

*   **route** — Route is a command line tool that allows a user to view and configure there operating system’s routing table.

[https://www.computerhope.com/jargon/r/route.htm](https://www.computerhope.com/jargon/r/route.htm)

*   **traceroute** — Traceroute is a method of sending a packet and tracing the packet from its starting to ending location and showing each of the hops required to get to the location. Example tool: tracert

**2\. Bootstrap commands —** Mach interface and stub generator.

**3\. Developer -cmds —** Install (ctags, haxdump, rpcgen, unifdef)

*   **ctags** — Create tag files for source code.tag file allows items to be quickly and easily located.

[http://www.tutorialspoint.com/unix\_commands/ctags.htm](http://www.tutorialspoint.com/unix_commands/ctags.htm)

*   **hexdump** — the hexdump utility is a filter which displays the specified files, or the standard input. If no files are specified, in a user-specified format.

[http://www.tutorialspoint.com/unix\_commands/hexdump.htm](http://www.tutorialspoint.com/unix_commands/hexdump.htm)

*   **rpcgen** — The rpcgen command generates C code to implement a Remote Procedure Call (RPC) protocol. The input to the rpcgen command is a language similar to C language known as RPC language.

[https://www.ibm.com/support/knowledgecenter/ssw\_aix\_71/com.ibm.aix.cmds4/rpcgen.htm](https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.cmds4/rpcgen.htm)

*   **unifdef** — The unifdef command is useful for removing ifdef lines from a file while otherwise leaving the file alone.

[https://www.ibm.com/support/knowledgecenter/es/ssw\_aix\_72/com.ibm.aix.cmds5/unifdef.htm](https://www.ibm.com/support/knowledgecenter/es/ssw_aix_72/com.ibm.aix.cmds5/unifdef.htm)

**4\. Diskdev-cmds —** Install (mount, quota, fsck, fstyp, fdisk, tunefs)

*   **mount** — mount is a storage device filesystem available for use by the computers OS, Mounting a storage device such as drive, allow that drive to be available to the OS, which gives the ability to view, copy, and manage the files on the drive.

[https://www.computerhope.com/jargon/m/mount.htm](https://www.computerhope.com/jargon/m/mount.htm)

*   **quota** — disk quota management are permission given to admin that set limits on the user, workgroups, or other groups of storage spaces.

[https://www.computerhope.com/jargon/d/diskqm.htm](https://www.computerhope.com/jargon/d/diskqm.htm)

*   **fsck** — fsck (File System Check) is a program run on Linux or UNIX and their variants which checks the file system for any errors.

fsck functions in two modes.

*   **interactive** — interactive mode prompts the user each time it finds the error to determine whether or not the user wants to fix the error or continue without fixing.
*   **Non-Interactive **— This automatically corrects errors without prompting the user.

[https://www.computerhope.com/jargon/f/fsck.htm](https://www.computerhope.com/jargon/f/fsck.htm)

*   **fstyp** — Filesystem type is a statement used in a Unix or Linux environment that declares the file system type being used or specified. for example, **hfs** and **swap** is fstype

[https://www.computerhope.com/jargon/f/fstype.htm](https://www.computerhope.com/jargon/f/fstype.htm)

*   **fdisk** — fdisk is a partition table manipulator for Linux

[https://www.computerhope.com/jargon/f/fdisk.htm](https://www.computerhope.com/jargon/f/fdisk.htm)

*   **tunefs** — tunefs command is helpful to manipulate the filesystem parameters of an ext2, or ext3, or ext4 type file system

[https://linux.101hacks.com/unix/tune2fs/](https://linux.101hacks.com/unix/tune2fs/)

**5\. Erica utilities —** A collection of command-line utilities for various purposes.

**6\. File-cmds — ** Install (chflags, compress, ipcrm, ipcs, pax)

*   **chflags** — Change a file or folder’s flag.

[https://ss64.com/osx/chflags.html](https://ss64.com/osx/chflags.html)

*   **compress** — Compress compacts a file so that it becomes smaller. When compressing a file it will be replaced with a file with extension .z, while keeping all the same ownership modes.
*   **ipcrm** — ipcrm command can be used to remove an IPC object from the kernel.

[https://www.tldp.org/LDP/lpg/node26.html](https://www.tldp.org/LDP/lpg/node26.html)

*   **ipcs** — Ipcs shows information on the inter-process communication facilities for which the calling process has read access.

[https://www.geeksforgeeks.org/ipcs-command-linux-examples/](https://www.geeksforgeeks.org/ipcs-command-linux-examples/)

*   **pax** — Short for portable archive interchange, the pax command read, writes, and write, and write the lists of members of the archive file and copy directory hierarchies.

**7\. Gawk — ** (GNU’s heavy-weight implementation of awk)

**8\. IOkit tools — ** (ioalloccount, ioclasscount,ioreg)

*   **ioalloccount** — ioalloccount displays some accounting of memory allocation by IOkit Tool's allocators, including object instances, in the kernel. useful for tracking leaks

[http://www.manpagez.com/man/8/ioalloccount/](http://www.manpagez.com/man/8/ioalloccount/)

*   **ioclasscount** — ioclasscount displays the instances count, offset by the number of subclasses that have at least one allocated, for the class specified.

[http://www.manpagez.com/man/8/ioclasscount/](http://www.manpagez.com/man/8/ioclasscount/)

**9\. Link identifier Editor —** This program lets you manipulate the signature block in a Mach-O binary. Use -S to sign a binary from scratch and allocate its entitlements, -s to update the hashes on an existing binary or, -e to dump entitlements.

Other Important Utilities and tools.

**10\. Make —** Dependency-based build environments.

**11\. Nano** — completely free, modern clone of pico

**12\. Unrar** — De-compresses files in rar format

**13\. Unzip** — De-Compresses files in zip format

**14. .Syslog Commandline** — Enable/disable Syslog via cmd line. syslogon to enable, syslogoff to disable. Log to /var/log/syslog

**15\. Zip** — Standard compression tool

**16\. OpenSSH** — Secure remote access between machines.

**17\. OpenSSL** — SSL library and cryptographic tools.

**18\. Apt 1.4 Strict ** — The advanced packaging tool from Debian

**19\. Git ** — Fast Content-addressable system

**20.** **PreferencesLoader** — PreferencesLoader is a MobileSubstrate based utility that allows developers to add entries to the settings up, Similar to the SettingsBundles that app store apps use.

**21\. AppList** — Allows developers to query the list of installed apps and provide a preferences pane based on that information.

Exports displayIdentifier, displayName, icon, and small-con via a remote messaging center so that it’s easy to write a prefs pane that presents a list of apps.

### Installing iOS Security Tools on MacOS

#### Installing iExplorer

iExplorer is the ultimate iPhone manager. It transfers music, messages, photos, files and everything else from any iPhone, iPod, iPad or iTunes backup to any Mac or PC computer. It’s lightweight, quick to install, free to try, and up to 70x faster and more resource efficient than the competition.

Downloading and uses of iExplorer.

iExplorer : [https://macroplant.com/downloads](https://macroplant.com/downloads)

![](https://cdn-images-1.medium.com/max/800/1*c1_ybEjvyNIz7AC6fXclbg.png)

After installing the iExplorer, we have to connect the iOS device to macbook with cable.

![](https://cdn-images-1.medium.com/max/800/1*9NQ6Xos3Aao4zEB4tVbdMQ.png)

Installed apps can be found using Apps tabs

![](https://cdn-images-1.medium.com/max/800/1*0Uohv27isDjuSkNdfgtTTQ.png)

We can also analyse the backups using iExplorer.

![](https://cdn-images-1.medium.com/max/800/1*N0U99O_YwGMxKKTIcu8KLw.png)
![](https://cdn-images-1.medium.com/max/800/1*0hh5-1lHIBNhBlny-TRvHg.png)

#### Installing Cydia Impactor —

Cydia Impactor is a GUI tool for working with mobile devices. It has features already, but is still very much a work-in-progress. It is developed by saurik.

Downloading & Installing Cydia Impactor. (Developers Account Required)

Cydia Impactor: [http://www.cydiaimpactor.com/](http://www.cydiaimpactor.com/)

Note: Cydia requires your Apple id and password, using newly created Apple id is recommended.

![](https://cdn-images-1.medium.com/max/800/1*cuHuvfOjt90_x_B3y5cqbg.png)

Installing ipa applications in iPhone using Cydia Impactor.

![](https://cdn-images-1.medium.com/max/800/1*oijc7uTkmd2cPYwdlAkZsg.png)

![](https://cdn-images-1.medium.com/max/600/1*eJ3SJu65chdmWCLl4mNfQw.png)
![Enter your Apple id credentials.](https://cdn-images-1.medium.com/max/600/1*ePvy13Zfj9gFD7FuOouVAg.png)


Enter your Apple id credentials.

I am getting the following error because I don’t have developers account.

![](https://cdn-images-1.medium.com/max/800/1*28aUqH3rR6LmUOqUtXzQOQ.png)

#### Burp Suite Free/Pro — Downloading and configuring.

Burp Suite is the industry-leading intermediate proxy tool, which is having huge no of tools and utility required to perform pentesting or security audit.

Download — [http://portswigger.net](http://portswigger.net)

**Setting Proxy lister — Proxy → Options → Proxy Listener → Add**

Bind to port: 1337

Bind to address : All interfaces (192.168.2.240)

Click “Ok”

![](https://cdn-images-1.medium.com/max/800/1*ddgGDLw5aDb1G_xMBRpKQg.png)

**Settings → wifi → (i) from connected network → Configure Proxy → Manual**

Server : 192.168.2.40

Port: 1337

![](https://cdn-images-1.medium.com/max/800/1*NfPe1Wjps67gihOLBLctzg.png)

Visit: [http://burp](http://burp) in Safari browser.

![](https://cdn-images-1.medium.com/max/800/1*wO3oEdPH9xpFBPQotQ_ZqQ.png)

Click on “CA Certificate” to download the certificate and click “allow”.

![](https://cdn-images-1.medium.com/max/800/1*fSMDWzVBzzGy7P_1O_xuDA.png)

Install the downloaded certificate.

![](https://cdn-images-1.medium.com/max/800/1*uKPNPskUscBHupbaRLFCew.png)

**Settings → about → Certificate Trust Settings**

Enable the trust for the root certificate

![](https://cdn-images-1.medium.com/max/800/1*RfzxzeAqikQA5SrM6I4Lyw.png)

Now, You should be able to intercept the HTTP and HTTPs traffic from the iOS device.

![](https://cdn-images-1.medium.com/max/800/1*h0E5MDSAUUG7JimbL67Onw.png)

#### Installing Hopper

Hopper is an excellent modern disassembler, decompiler, and debugger. The control flow graph and pseudo code feature.

* [**Hopper** ](https://www.hopperapp.com/ "https://www.hopperapp.com/")[](https://www.hopperapp.com/)

#### Installing IDA

IDA is a Windows, Linux or Mac OS X hosted multi-processor disassembler and debugger that offers so many features it is hard to describe them all. Just grab an [evaluation version](https://www.hex-rays.com/products/ida/support/download.shtml) if you want a test drive.

* [**IDA: About** ](https://www.hex-rays.com/products/ida/ "https://www.hex-rays.com/products/ida/")[](https://www.hex-rays.com/products/ida/)

### External Tools/Apps Installation for iOS devices.

Commands you should know, before proceeding.

**scp** — Secure copy(scp) — **scp** allows files to be copied to, from, or between different hosts. It uses **ssh** for data transfer and provides the same authentication and same level of security as **ssh**.

[https://www.hypexr.org/linux\_scp\_help.php](https://www.hypexr.org/linux_scp_help.php)

**uicache** — Removing or update application logo from ui caches

[https://stackoverflow.com/questions/44605125/what-does-uicache-command-do-on-jailbreak-iphone](https://stackoverflow.com/questions/44605125/what-does-uicache-command-do-on-jailbreak-iphone)

**ssh** — **Secure Shell**, **SSH** (developed by SSH Communications Security Ltd.) is a secure protocol for remote logins. Using an SSH client, a user can connect to a server to transfer information in a more secure manner than other methods, such as [telnet](https://www.computerhope.com/jargon/t/telnet.htm).

[https://www.computerhope.com/jargon/s/ssh.htm](https://www.computerhope.com/jargon/s/ssh.htm)

**dpkg** — **Debian Package Manager**, **dpkg** is a [software package](https://www.computerhope.com/jargon/p/packsoft.htm) installation and management tool.

[https://www.computerhope.com/jargon/d/dpkg.htm](https://www.computerhope.com/jargon/d/dpkg.htm)

**chmod** — **chmod** is used to change the [permissions](https://www.computerhope.com/jargon/p/permissi.htm) of [files](https://www.computerhope.com/jargon/f/file.htm) or [directories](https://www.computerhope.com/jargon/d/director.htm).

[https://www.computerhope.com/unix/uchmod.htm](https://www.computerhope.com/unix/uchmod.htm)

**mv** — The **mv** command moves, or renames, files and directories on your filesystem.

**cp** — The **cp** command is makes copies of files and directories.

[https://www.computerhope.com/unix/ucp.htm](https://www.computerhope.com/unix/ucp.htm)

#### **SSH to the iOS device.**

SSH is the secure shell used to connect to different machines.

1.  Finding the IP address of the device.

**Settings → Connected Network → Click on (i)**

![](https://cdn-images-1.medium.com/max/800/1*vO-fJ_IzLb1EG96o76JZkg.png)

IP address of the device — 192.168.2.41

2\. Available Users on the iOS device.

**mobile** — default password — alpine

**root** — default password — alpine

3\. Connecting as mobile and getting root privileges.

`**ssh** mobile@192.168.2.41`

password=alpine // you should change it using passwd utility

![](https://cdn-images-1.medium.com/max/800/1*Lcb9yJcMT7g48ox6zzwFHg.png)

Getting root privilege

`**su**`

password = alpine (you should also change it)

![](https://cdn-images-1.medium.com/max/800/1*1y9as0yTd6ty-N6-Mx5Zwg.png)

Changing Default Password

`**passwd**`

New password:<new-password>  
Retype new password:<retype-new-password>

![](https://cdn-images-1.medium.com/max/800/1*ilcayAl5M_c8PPP3CIpaeQ.png)

#### Installing Class-Dump

Class-dump — [https://github.com/ehsahil/Class-dump-z-backup](https://github.com/ehsahil/Class-dump-z-backup)

Note: NOT supported in iOS 11, If you guys found working one, please let me know.

`**scp** -r class-dump-z.zip root@192.168.2.41:~`

password: alpine (default)

`**ssh** root@192.168.2.41`  
password:alpine (default)

`**unzip** class-dump-z.zip`

![](https://cdn-images-1.medium.com/max/800/1*lpues5MS77KfkaiyKF8pFQ.png)

`**cd** class-dump-z/iphone\_armv6`

`**cp** class-dump-z /usr/bin //copying class-dump-z to /usr/bin   
class-dump-z`

![](https://cdn-images-1.medium.com/max/800/1*wk_LAP-IkkCTlNnm-dBYAA.png)

ERROR: sh:/usr/bin/class-dump-z: Bad CPU type in executable.

**Unfortunately** — Class-dump is also not supported by the iOS 11.2.6 :(

I’ve kept the installation instructions because maybe your version supports it.

#### Installing Clutch.

_Clutch_ is a high-speed iOS decryption tool. Clutch supports the iPhone, iPod Touch, and iPad as well as all iOS version, architecture types, and most binaries.

Github Repository: [https://github.com/KJCracks/Clutch](https://github.com/KJCracks/Clutch)

For installation instructions please refer to above Github repository.

Killall Xcode

![](https://cdn-images-1.medium.com/max/800/1*uehy1aVmwdO8LAWCwgivfA.png)

`git clone [https://github.com/KJCracks/Clutch.git](https://github.com/KJCracks/Clutch.git)`  
`cd Clutch` 
`xcodebuild clean build`

![](https://cdn-images-1.medium.com/max/800/1*0T73vFsCXe9DMDZQa8aV_g.png)
![](https://cdn-images-1.medium.com/max/800/1*hHYq2GXx5FMNDU2_cIuxYw.png)

run the following command under the build directory.

scp -r Clutch root@<Ip-address-of-ios-device>:~
  
`scp -r Clutch root@192.168.2.41:~`

`ssh root@192.168.2.41`  

password:alpine

`cp Clutch /usr/bin`

![](https://cdn-images-1.medium.com/max/800/1*ZaYaogrXYSADJOJq2W01RA.png)

`Clutch`

![](https://cdn-images-1.medium.com/max/800/1*7lc9XK7yPirbhRvt25dDBw.png)

#### Installing Introspy iOS

Blackbox tool to help understand what an iOS application is doing at runtime and assist in the identification of potential security issues.

Github: [https://github.com/iSECPartners/Introspy-iOS](https://github.com/iSECPartners/Introspy-iOS)

Download the Debian package from the above repository.

Copying the Debian file into the iOS device.

`scp -r com.isecpartners.introspy-v0.5.1-iOS\_9.deb root@192.168.2.41:~`

password:alpine

![](https://cdn-images-1.medium.com/max/800/1*HiZHyVpoj-baI1fEnglQhA.png)

`dpkg -i com.isecpartners.introspy-v0.5.1-iOS\_9.deb`

![](https://cdn-images-1.medium.com/max/800/1*YCG1_2uGITdeTOjJ9vA36Q.png)

Successfully installed.

#### Installing SSL KILL Switch 2

Blackbox tool to disable SSL certificate validation — including certificate pinning — within iOS and OS X Apps.

Github Repository — [https://github.com/nabla-c0d3/ssl-kill-switch2](https://github.com/nabla-c0d3/ssl-kill-switch2/releases)

`**scp** -r com.nablac0d3.sslkillswitch2\_0.12.deb root@192.168.2.41:~`

`**ssh** root@192.168.2.4`1

`**dpkg** -i com.nablac0d3.sslkillswitch2\_0.12.deb`

![](https://cdn-images-1.medium.com/max/800/1*JPpt_RbiAHMwy89gezzHXw.png)

Successfully installed.

Let’s talk about Damn Vulnerable iOS Application (**DVIA**)

[**DVIA (Damn Vulnerable iOS App) - A vulnerable iOS app for pentesting**  
_Swift Version (April, 2018) - Download the IPA file from here Github - Here Make sure to read this for…_damnvulnerableiosapp.com](http://damnvulnerableiosapp.com/ "http://damnvulnerableiosapp.com/")[](http://damnvulnerableiosapp.com/)

Damn Vulnerable iOS App (DVIA) is an iOS application that is damn vulnerable. Its main goal is to provide a platform to mobile security enthusiasts/professionals or students to test their iOS penetration testing skills in a legal environment. Created By [Prateek Gianchandani](https://twitter.com/prateekg147) (@prateekg147).

#### Installing Damn Vulnerable iOS Application (Version -1)

Github Repository — [https://github.com/prateek147/DVIA](https://github.com/prateek147/DVIA)

Download the .ipa file and Open with “Archive Utility‘.

![](https://cdn-images-1.medium.com/max/800/1*WVCZKGJEXI8SsJF58u5Hdw.png)

You will have extracted folder and you will get payload folder with “**DamnVulnerableIOSApp**”.

We need to move this to the iOS device.

![](https://cdn-images-1.medium.com/max/800/1*kjxT1EstMHHaFUjP0zKZdw.png)

**pwd** // print work directory. 

/Users/sahil/Desktop

`**scp** -r /Users/sahil/Desktop/DamnVulnerableIOSApp.app mobile@192.168.1.1:~`

![](https://cdn-images-1.medium.com/max/800/1*Ix4kCkG9nhmO7I5orCyCxg.png)

Password : alpine (default)

![](https://cdn-images-1.medium.com/max/800/1*QIXHNg1EM5qsBspQLl9iHA.png)

`**ssh** mobile@192.168.1.170`

**Password**: alpine

![](https://cdn-images-1.medium.com/max/800/1*eWT2GFJt8OwEOVb4PiX5Gw.png)

`**su**`

password: alpine

**ls**

`**mv** DamnVulnerableIOSApp.app /Applications/`

![](https://cdn-images-1.medium.com/max/800/1*hXmJftG7cH1AZFITbI2AIg.png)

`**cd** /Applications`

![](https://cdn-images-1.medium.com/max/800/1*8whzLuXKy_8jXl3dbD1OXg.png)

`**cd** /DamnVulnerableIOSApp.app`

![](https://cdn-images-1.medium.com/max/800/1*1e7r6KrfylSAIpCjPoyUwA.png)

Giving root execution permission to DamnVulnerableIOSApp.

`**chmod** +x DamnVulnerableIOSApp`

`**exit** //changing from root to mobile`

`**uicache**` 

![](https://cdn-images-1.medium.com/max/800/1*a2Kf5EMCxLVcwRvHICIYQw.png)

After finishing “uicache”, You should be able to see the DVIA version-1 in your apps.

![](https://cdn-images-1.medium.com/max/800/1*yCAgAAqyTy9j7kdUFoYxQg.png)

#### DVIA Version 2 Installation — Similar to Version 1

Github Repository: [https://github.com/prateek147/DVIA-v2](https://github.com/prateek147/DVIA-v2)

Installation of the version 2 is also same, I recommend doing it because you will be more familiar with the process.

`scp -r DVIA-v2.app mobile@192.168.1.170:~`

![](https://cdn-images-1.medium.com/max/800/1*1RtY3w5bBSUZDnfqNtAbsw.png)

`**ssh** mobile@192.168.1.170`

password: alpine

**su**

password: alpine

![](https://cdn-images-1.medium.com/max/800/1*e623cXSxW8exvig5DzjICw.png)

**ls** //seeing the file is successfully copied into the device.

moving the Damn-v2.app from root directory to /Applications.

`**mv** DVIA-v2.app/ /Applications/`

![](https://cdn-images-1.medium.com/max/800/1*-aT74FtgvZIgrSmVmxIZLA.png)

`**cd** /Applications/DVIA-v2`

![](https://cdn-images-1.medium.com/max/800/1*QzEgsM_j5jZIYul_3Siz2A.png)

Changing the executable permissions.

`**chmod** +x DVIA-v2`

`exit`

![](https://cdn-images-1.medium.com/max/800/1*0eDNxZfxfaSQrEodYkZv-Q.png)

`**uicache**`

![](https://cdn-images-1.medium.com/max/800/1*RkkSwR1OJfQuzzf8O9DamA.png)

After finishing “uicache”, You should be able to see the DVIA version-1 in your apps.

![](https://cdn-images-1.medium.com/max/800/1*Srlh4-qLsZ4kCraRqkeKKw.png)

#### File Explorer / iFile — Not supported in iOS 11.2.6

I got the iFile from the mega link provided in the following blog post.

* [**Download iFile IPA on iOS 12/11+(iPhone/iPad) Without Jailbreak 2018**  ](https://igeeksradar.com/ifile-ios/ "https://igeeksradar.com/ifile-ios/")[](https://igeeksradar.com/ifile-ios/)

Use the following iFile with your own risk, I don’t know it is from the trusted source or not.

* [**MEGA** ](https://mega.nz/#!QV1WXJzY!gIl_PimOwwdZGn1d87N2SryCEeo32DkudhKAC7-KGCc "https://mega.nz/#!QV1WXJzY!gIl_PimOwwdZGn1d87N2SryCEeo32DkudhKAC7-KGCc")[](https://mega.nz/#!QV1WXJzY!gIl_PimOwwdZGn1d87N2SryCEeo32DkudhKAC7-KGCc)

`**scp** -r iFile.app mobile@192.168.170:~`

![](https://cdn-images-1.medium.com/max/800/1*UALGTOTyCF488JYR0YWZkQ.png)

`**ssh** mobile@192.162.1.170`

![](https://cdn-images-1.medium.com/max/800/1*-kG6wkP3IHZPra_QGdmstA.png)

`**mv** iFile.app/ /Applications/`

![](https://cdn-images-1.medium.com/max/800/1*knR6vHOSQkHrrEhNZjTT1A.png)

`**chmod** +x iFile`

![](https://cdn-images-1.medium.com/max/800/1*OHjiFFowdOIYC9yewFSd9g.png)

`**exit**`  
`**uicache**`

![](https://cdn-images-1.medium.com/max/800/1*C4Gi2lhdNZtjMNHQWnAE3g.png)
![](https://cdn-images-1.medium.com/max/800/1*96s7SLsDv8gfDwZxaM7JNQ.png)
![](https://cdn-images-1.medium.com/max/800/1*yUhlvdJ8r20vQYEL6AS7Pw.png)

But. unfortunately, the devs have not updated the iFile app to work with iOS 11.

I’ve kept the installation instructions because maybe your version supports it.

**If you guys find the working iFile app version for 11.2.6 let me know.**

This post is getting too long and there many things to be added.

In the mean time you can learn from the intensive iOS security guide.

* [**iOS Application security Part 1 - Setting up a mobile pentesting platform - Prateek Gianchandani**](http://highaltitudehacks.com/2013/06/16/ios-application-security-part-1-setting-up-a-mobile-pentesting-platform/ "http://highaltitudehacks.com/2013/06/16/ios-application-security-part-1-setting-up-a-mobile-pentesting-platform/")[](http://highaltitudehacks.com/2013/06/16/ios-application-security-part-1-setting-up-a-mobile-pentesting-platform/)

**I’m planning to cover the following things in up coming posts.**

*   Understanding the Architecture of the iOS application.
*   installing and Configuring Introspy iOS
*   SSL KILL Switch 2
*   Using iExplorer
*   Using Hopper and IDA
*   Using Clutch and Class-dump
*   Other tools installation and configurations.
*   Your Recommendations
*   **Security Issues In Damn Vulnerable iOS application V-1**

1.  Insecure Data Storage
2.  Jailbreak Detection
3.  Runtime Manipulation
4.  Sensitive information in memory
5.  Privacy detection
6.  Security Decision via untrusted input.
7.  Side channel Data leakage
8.  Transport Layer Security
9.  Client Side security
10.  Broken Cryptography
11.  Binary patching

*   **Security Issues In Damn Vulnerable iOS application V-2**

1.  Local Data Storage
2.  Jailbreak Detection
3.  Excessive Permissions
4.  Runtime Manipulation
5.  Anti anti Hooking/Debugging
6.  Binary Protection
7.  Touch/Face ID Bypass
8.  Phishing
9.  Side Channel Data leakage
10.  IPC issues
11.  Broken Cryptography
12.  WebView issues
13.  Network Layer Security
14.  Application Patching
15.  Sensitive Information is Memory
16.  Data Leakage to Third parties

#### Credits and References.

I do not own any tools and Utilities listed in this blogpost. Every tool belongs to their respective owners.

[Prateek Gianchandani](https://twitter.com/prateekg147)

[**DVIA (Damn Vulnerable iOS App) - A vulnerable iOS app for pentesting**](http://damnvulnerableiosapp.com/#downloads "http://damnvulnerableiosapp.com/#downloads")[](http://damnvulnerableiosapp.com/#downloads)

[SecurityInnovation.com](https://web.securityinnovation.com/hubfs/iOS%20Hacking%20Guide.pdf)

Until next Time.
