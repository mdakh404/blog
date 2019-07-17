---
title: Basic Android Security Testing lab — 1
description: 'Hi Everyone,'
date: '2018-08-03T00:13:46.785Z'
categories: []
keywords: []
slug: /@ehsahil/basic-android-security-testing-lab-part-1-a2b87e667533
---

Hi Everyone,

Actually, I was creating a new Android application testing lab for myself and thought to document the whole process. There is nothing extraordinary in this post just a simple lab setup up guide.

**Why using Genymotion, not a physical device?**

I generally prefer the physical device over Genymotion but Genymotion have Android version flexibility advantage and Genymotion will also cover most of the researchers that’s why using it to document the process.

#### Summary

1.  Downloading all the things
2.  Downloading Devices in Genymotion
3.  Common Genymotion Configuration issue.
4.  Installing Google Play Services
5.  Configuring Device with Burp Suite.
6.  Downloading and installing Applications
7.  Common Android Debug Bridge (ADB) uses.
8.  Basic SSL Pinning Bypass setup

### 1\. Downloading all the things.

**Genymotion**: Download Genymotion Personal Edition.

[**Account Login - Genymotion Android Emulator**  
_We are using cookies to provide statistics that help us give you the best experience of our site. By continuing to use…_www.genymotion.com](https://www.genymotion.com/download/ "https://www.genymotion.com/download/")[](https://www.genymotion.com/download/)

**Virtual Box**: Download virtual-box.

[**Downloads - Oracle VM VirtualBox**  
_About Screenshots Downloads Documentation End-user docs Technical docs Contribute Community_www.virtualbox.org](https://www.virtualbox.org/wiki/Downloads "https://www.virtualbox.org/wiki/Downloads")[](https://www.virtualbox.org/wiki/Downloads)

**Burp Suite**: You can use the Free version but Pro is recommended.

[**Web Application Security, Testing, & Scanning | PortSwigger**  
_PortSwigger offers tools for web application security, testing & scanning. Choose from a wide range of security tools &…_portswigger.net](https://portswigger.net "https://portswigger.net")[](https://portswigger.net)

**Android Platform Tools:** Installing ADB and other android tools.

A. Install Homebrew

**_Sahils-MacBook-Pro:~ sahil$_**  **_ruby -e “$(curl -fsSL_** [**_https://raw.githubusercontent.com/Homebrew/install/master/install_**](https://raw.githubusercontent.com/Homebrew/install/master/install)**_)"_**

![](https://cdn-images-1.medium.com/max/800/1*RrlZw72sCNu_bLiJLVL0Lw.png)

B. Install Android Platform tools.

**_Sahils-MacBook-Pro:~ sahil$ brew install android-platform-tools_**

![](https://cdn-images-1.medium.com/max/800/1*57sv0o36Vi8dsLqYpK8JFw.png)

C. Verify Installation.

**Sahils-MacBook-Pro:~ sahil$ _adb devices_**

![](https://cdn-images-1.medium.com/max/800/1*P53RaZ37T7x2caa6X8f8fw.png)

### 2\. Downloading Device in Genymotion

I use multiple versions of android devices according to requirements and need.

![Select the device you want to install.](https://cdn-images-1.medium.com/max/800/1*I7Utc_unpModsDnl5uPukA.png)
Select the device you want to install.![Verify the configuration- You can always change them from Virtual Box.](https://cdn-images-1.medium.com/max/800/1*2n-eIlWBvQj6Buya33G-Cg.png)
Verify the configuration- You can always change them from Virtual Box.

### **3\. Common Genymotion Configuration issue.**

#### **ADB connection issue.**

Downloading and and installing.

Android SDK — [https://developer.android.com/studio/](https://developer.android.com/studio/)

![](https://cdn-images-1.medium.com/max/800/1*nTkFVdBCx2EjrUoyIJwMjw.png)

Find your Android SDK tools location and change the settings to use custom Android SDK tools in Genymotion.

file location for my machine. **_/Users/sahil/Library/Android/sdk_**

![](https://cdn-images-1.medium.com/max/800/1*EHBr7iBSXImqWc1c5oHEBw.png)

#### **External APK not installing/ARM installation issue.**

![](https://cdn-images-1.medium.com/max/800/1*s5ly9IWhYqD9La6nqW5QSA.png)

Download and flash the Genymotion-ARM-Translation.

Download it from My Dropbox link: [https://www.dropbox.com/s/k57l9uvyjy8gzxt/Genymotion-ARM-Translation\_v1.1.zip?dl=0](https://www.dropbox.com/s/k57l9uvyjy8gzxt/Genymotion-ARM-Translation_v1.1.zip?dl=0)

After install ARM Translation:

![](https://cdn-images-1.medium.com/max/800/1*zlLxfbPQjYbzouciGcj1dA.png)

### 4\. Install Google Play Services.

After boot-up see the upper right corner and select “Open Gapps”

That will automatically install all the Google Application required including Play store.

![See play store is installed in the virtual Device.](https://cdn-images-1.medium.com/max/800/1*beoLV7Syr57sDX1u9_JbyQ.png)
See play store is installed in the virtual Device.

### 5\. Configuring Device with Burp Suite

#### Add a proxy in Burp Suite to listen.

Address: **192.168.56.1** & Port: **1337**

Choose **_All Interfaces_** option.

![](https://cdn-images-1.medium.com/max/800/1*0Bn7HvqI775Nr5fXGcqoJA.png)

#### **Adding listener in Android device.**

Setting → Wifi →WiredSSID (Long press)

Choose Modify network → Check Advance options.

Select Proxy to the manual

![](https://cdn-images-1.medium.com/max/800/1*gkDuYqWMldFuYguQuID7sw.png)

Testing connection over http and https using devices browser.

1.  http:// (working) tested — [http://ehsahil.com](http://ehsahil.com)

![](https://cdn-images-1.medium.com/max/800/1*LJ2uhK2JqKYY_wYkH3jwbw.png)

2\. https:// certificate error — https://google.com

![](https://cdn-images-1.medium.com/max/800/1*M-AoG6Yqo21D9qgQHLCSzQ.png)

#### **Installing burp certificate in android device.**

Download burp certificate. — Use your desktop machine to download the certificate.

[https://burp](http://burp)

![](https://cdn-images-1.medium.com/max/800/1*f4LjnkNs7oA1f4XokEeiTw.png)

Click on **CA certificate download the certificate.**

The downloaded certificate is in cacert.der extension and android 5.\* does not recongnize it as certificate file.

You can download the cacert file using your desktop machine and rename it from cacart.der to cacert.crt and drop it on android device and certificate will be automatically added into **file:///sd\_card/downloads.**

**Installing the downloaded certificate.**

Settings →Security →Install certificate from SD cards

Now, goto: sdcard →Downloads → Select cacrt.crt

Now, Name it as anything “portswigger”

![](https://cdn-images-1.medium.com/max/800/1*lDtlQ1FfcHEytrSZNvs2Mw.png)

You also need to setup the PIN before adding certificate. Verifying the installed certificate using trusted certificates.

Trusted certificates →Users

![](https://cdn-images-1.medium.com/max/800/1*dvEffIIS0-dPE6q3ycFx3Q.png)

After installing Certificate SSL endpoints also working fine tested using → [https://google.com](https://google.com)

![](https://cdn-images-1.medium.com/max/800/1*lt0ZvZH60HI0ud1eE9jAnA.png)

### **6\. Downloading and Installing Applications**

You can use play store available in the device as well as the external services to download applications to play with.

For Downloading Application Externally, I generally use.

[**APK Downloader \[Latest\] Download Directly | Chrome Extension v3 (Evozi Official)**  
_Download APKs Directly From Google Play To Your Computer With APK Downloader Extension For Google Chrome_apps.evozi.com](https://apps.evozi.com/apk-downloader/ "https://apps.evozi.com/apk-downloader/")[](https://apps.evozi.com/apk-downloader/)

Add your testing Google account in Google Play Store to download apps.

![](https://cdn-images-1.medium.com/max/800/1*HLAWSaNBwJt6Gj7ztC5e8Q.png)

Download applications and start testing. (No Certificate pinning apps)

![Ola Lite application](https://cdn-images-1.medium.com/max/800/1*CO7KBGdE0bLemkLhkNwKQg.png)
Ola Lite application

### 7\. Common Android Debug Bridge (**ADB**) uses.

#### Connecting ADB with Genymotion device.

**_Sahils-MacBook-Pro:~ sahil$ adb connect 192.168.56.101:5555_**

![](https://cdn-images-1.medium.com/max/800/1*P53RaZ37T7x2caa6X8f8fw.png)

Device address can be found on the top right corner of the device.

![](https://cdn-images-1.medium.com/max/800/1*zs8eOJ4dd7TRQ_28Y3qhBg.png)

#### Installing APK files using ADB.

**_Sahils-MacBook-Pro:~ sahil$ adb install <you-apk-file-path/file.apk>_**

![](https://cdn-images-1.medium.com/max/800/1*GcP5jAlMJB35fGuqPNkfDQ.png)

#### Getting Shell on the device for manual analyses.

**_Sahils-MacBook-Pro:~ sahil$ adb shell_**

![](https://cdn-images-1.medium.com/max/800/1*upt-qWpH8yFzsENTCZj0JA.png)

#### Manual analysis of the installed application.

You will find all the installed applications in **/data/data** folder.

**_root@vbox86p:/ # cd /data/data_**

![](https://cdn-images-1.medium.com/max/800/1*m2KxHChNyGl2ASHRGhXmtA.png)

### 8\. Basic SSL Pinning Bypass setup

#### Common Tools

**Frida**

**_Sahils-MacBook-Pro:~ sahil$ sudo pip install frida-tools_**

**Objection-** Objection uses the Frida and automate the process to bypass the certificate pinning.

**_Sahils-MacBook-Pro:~ sahil$ sudo pip3 install objection_**

#### **Application with SSL Pinning**

Taking the example of Twitter Application. This setup is not able to intercept the request for Twitter application.

When I tried to log in with intercept ON.

![](https://cdn-images-1.medium.com/max/800/1*3hye_wW2_hHa2ykdj-u-gA.png)

Got an Error “**An error occurred when logging in. Please try again later**”

Burp Alert logs giving back the following error.

**_The client failed to negotiate an SSL connection to api.twitter.com:443: Received fatal alert\_certificate\_unknown_**

![](https://cdn-images-1.medium.com/max/800/1*TvvEUDvusUi3ZvWwRivEfA.png)

Burp Suite is not able to intercept the twitter applications request because twitter using SSL pinning to not allow someone to intercept the request.

We have to bypass the SSL Pinning to intercept the twitter applications traffic.

#### **Bypassing SSL Pinning using Objection tool.**

Objection is a great tool, which automates most of the process to bypass the SSL Pinning.

1.  Downloading Twitter APK from Google Play Store or External providers.
2.  Objection command to bypass SSL Pinning.

**_Sahils-MacBook-Pro:Downloads sahil$ sudo objection patchapk -s com.twitter.android.apk_**

![](https://cdn-images-1.medium.com/max/800/1*9DwpdqCh1kzIAgfmlh9_ng.png)

3\. Installing objection output APK **com.twitter.android.objection.apk** to the device using ADB.

![](https://cdn-images-1.medium.com/max/800/1*zqjognKtW0Zp5gb-DL3slQ.png)

PS: This method/tool doesn’t work on all the android applications**\***

**Interesting resources to follow.**

[**Mobile Security Wiki**  
_AppMon - AppMon is a runtime security testing & profiling framework for macOS, iOS and android apps. It is useful for…_mobilesecuritywiki.com](https://mobilesecuritywiki.com/ "https://mobilesecuritywiki.com/")[](https://mobilesecuritywiki.com/)

[**The Stony Path of Android 🤖 Bug Bounty - Bypassing Certificate Pinning**  
_Dear readers, Long story short, doing bug bounties for mobile devices is hard. With this article I want to show you a…_blog.it-securityguard.com](https://blog.it-securityguard.com/the-stony-path-of-android-%F0%9F%A4%96-bug-bounty-bypassing-certificate-pinning/ "https://blog.it-securityguard.com/the-stony-path-of-android-%F0%9F%A4%96-bug-bounty-bypassing-certificate-pinning/")[](https://blog.it-securityguard.com/the-stony-path-of-android-%F0%9F%A4%96-bug-bounty-bypassing-certificate-pinning/)

[**Bypassing SSL Pinning in Android Applications**  
_It is a common practice for Android and iOS applications' developers to implement SSL Pinning in order to make reverse…_serializethoughts.com](https://serializethoughts.com/2016/08/18/bypassing-ssl-pinning-in-android-applications/ "https://serializethoughts.com/2016/08/18/bypassing-ssl-pinning-in-android-applications/")[](https://serializethoughts.com/2016/08/18/bypassing-ssl-pinning-in-android-applications/)

[**Four Ways to Bypass Android SSL Verification and Certificate Pinning**  
_As pentesters, we'd like to convince the app that our certificate is valid and trusted so we can man-in-the-middle…_blog.netspi.com](https://blog.netspi.com/four-ways-bypass-android-ssl-verification-certificate-pinning/ "https://blog.netspi.com/four-ways-bypass-android-ssl-verification-certificate-pinning/")[](https://blog.netspi.com/four-ways-bypass-android-ssl-verification-certificate-pinning/)

[**Using Frida on Android without root · John Kozyrakis ~ blog**  
_Frida is a great toolkit by @oleavr, used to build tools for dynamic instrumentation of apps in userspace. It is often…_koz.io](https://koz.io/using-frida-on-android-without-root/ "https://koz.io/using-frida-on-android-without-root/")[](https://koz.io/using-frida-on-android-without-root/)

**If you like my blog posts and my work, Please consider checking out my “Buy me a coffee” page**

[**Buy Me A Coffee - Best Way for Creators to Receive Tips**  
_Buy Me A Coffee help creators receive support from their audience in a friendly manner. Quickly accept donations and…_www.buymeacoffee.com](https://www.buymeacoffee.com/ehsahil "https://www.buymeacoffee.com/ehsahil")[](https://www.buymeacoffee.com/ehsahil)

#### Part-2 — I will include most of the available certificate pinning bypasses. Until next time.