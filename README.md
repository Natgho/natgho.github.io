# Quick App with Push Kit Codelab
## Table of Contents
 * [Introduction](#introduction)
 * [Installation](#installation)
 * [Configuration ](#configuration )
 * [Supported Environments](#supported-environments)
 * [License](#license)

## Introduction
Quick apps are a new form of installation-free apps developed based on industry standards. They are developed based on the frontend technology stack and support native rendering, therefore possessing the advantages of both HTML5 apps and native apps. Users do not need to install quick apps and only need to tap them to open and enjoy the same experience and performance as native apps. In this way you can create Quick App and send push notification to users for news or another information.
### What You Will Create

In this codelab, you will use the demo project that has been created for you to experience Quick App and Push Kit integration. Through the demo project, you will experience developing a simple push notification on a Quick application;

- Create Quick App
- Integrate HMS Push Kit
- Send data and push notification using AppGalleryConnect

### What You Will Learn

In this codelab, you will learn how to:

- Integrate and use abilities of Push Kit on a Quick App 
- Using Huawei Quick App IDE to achieve H5 applications and integrate Push Kit

## Installation
### Required Knowledge

- Javascript and CSS

1. Installing Huawei Quick App IDE
   - Install Node.js.
      If you have not installed Node.js or your Node.js version is earlier than version 6, go to [NodeJS official website](https://nodejs.org/en/) and download and install it.
   - Obtain installation package.([Version Update Introduction](https://developer.huawei.com/consumer/en/doc/quickapp-ide-vdd))
      Win64: [DevecoQuickAppIDE-V2.6.2NonChina-Win.exe](https://appfile1.hicloud.com/FileServer/getFile/appAttach/011/111/111/0000000000011111111.20200829101405.23973388354629496506234801230073:20471231000000:0001:EB03AC4B342CDE671C6CB407310A1FC047BBFC82BA2F7706DA19C6886635986D.exe?needInitFileName=true) (207 MB)
      Mac: [DevecoQuickAppIDE-V2.6.2NonChina-Mac.dmg](https://appfile1.hicloud.com/FileServer/getFile/appAttach/011/111/111/0000000000011111111.20200829101604.71853738336768095592986248706334:20471231000000:0001:0AC6A8D9E8E3B9872255AA6353AD058E3627ACC36B8FD85F5DE1D2425C715300.dmg?needInitFileName=true) (314 MB)
   - Install Huawei quick app IDE.
      Win64: Click **DevecoQuickAppIDE-V2.6.2NonChina-Win.exe** to start installation. The installation will automatcially uninstall  the earlier version.
      Mac: See the [Installing Huawei QuickApp IDE on Mac](https://developer.huawei.com/consumer/en/doc/quickapp-ide-install-mac).
   - 

## Supported Environments
### Hardware Requirements

- One computer (with Quick App IDE installed)
- One Huawei phone (with a USB cable) is used to run applications in EMUI 8.0 or later.

### Software Requirements

- Node.js 6 or later has been installed on the PC. (Note: Do not use V8.0.X, whose ZipStream implementation is incompatible with node-archive. Otherwise, an error will occur.)
- Install the latest Quick App IDE version on the PC.

## Configuration 
### Creating Quick App

**Step 1:** Create an app on AppGallery Connect. Don’t forget to select QuickApp option as the Platform type.
**Step 2:** Select data storage location into Project Settings Page.
**Step 3:** Enable Push Kit under project Settings>Growing>Push Kit then select your data storage location.
**Step 4:** Open the Huawei quick app IDE and go to File > New project > New QuickApp Project.
**Step 5:** Create certificate for using AGC and integrating HMS Push Kit.
**Step 6:** Copy generated certificate fingerprint and paste it into your project settings page to AGC.
**Step 7:** Paste this generated fingerprint to Application certificate into AGC Project Settings "SHA-256 certificate fingerprint" section.

### Integrating HMS Push Kit in the Quick App

**Step 1:** Add the following configuration to the features attribute in the manifest.json file:

```json
{"name": "service.push"}
```

**Step 2:** Add the following configuration to the "\<script>"  on the page where the API will be called. You must add this to be able to use push functions on the page.

```javascript
 import push from '@service.push'
```

**Step 3:** To send push notifications, you must have a token. In order to receive tokens, you must add the subscribe function to your application.

```javascript
push.subscribe({
    success: function(data) {
        console.log("push.subscribe succeeded, result data=" + JSON.stringify(data));
    },
    fail: function(data, code) {
        console.log("push.subscribe failed, result data=" + JSON.stringify(data) + ", code=" + code);
    },
    complete: function() {
        console.log("push.subscribe completed");
    }
});

```


##  License
    Videokit Codelab is licensed under the [Apache License, version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

