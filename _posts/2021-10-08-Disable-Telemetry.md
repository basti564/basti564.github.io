---
title: Prevent FaceBook from spying on you
layout: post
description: This tutorial will show you how to disable Telemetry on your Oculus Quest (2)
tags: post oculus quest telemetry facebook tutorial
minute: 1
---

## Video Tutorial
If you prefer a video tutorial you can watch [this one](https://www.youtube.com/watch?v=ArXk_hob4RE) I made back in april, but please read the pinned comment as it's a little outdated.

## What is Telemetry?
Telemetry refers to FaceBook gathering data on the performance of your Quest and on how you use it. With that come serious privacy concerns as FaceBook isn’t exactly known to respect the privacy of their users. Also while probably not noticable, telemetry can and will impact your battery usage and performance to some degree.

##### Side effects
Disabeling Telemetry has little sideeffect, the only ones known so far are
- Fitness tracking not working
- You won't be able to remove Oculess from your device (without a factory reset)

### Sideloading the APK
If you already know how to sideload an APK to the Quest, just download the APK from step 1.
1. Download the Oculess.apk from [here](https://github.com/basti564/Oculess/releases)
2. Follow this [Video Guide](https://youtu.be/RoIXxIfRNTw?t=125) by "Virtual Reality Oasis"
3. Click this icon in SideQuest 

![Install APK from folder](/assets/images/posts/install.PNG)
4. Select the APK file you have downloaded in step 1
5. Wait for the upload to finish

### Temporarily remove accounts
1. Open the app
2. Click the "REMOVE ACCOUNTS" button
3. Click "OK" and a settings page should appear
4. Select the accounts on your device (most likely only Oculus and Facebook accounts)
5. Use the "REMOVE ACCOUNT" option for the accounts.

### Make Oculess Device Owner
1. Again open up SideQuest
2. Click on this icon in SideQuest

![Run ADB commands](/assets/images/posts/adb.PNG)
3. Select "CUSTOM COMMAND" from the dropdown menu
4. Enter the following command
```
adb shell dpm set-device-owner com.bos.oculess/.DevAdminReceiver
```
5. Click "RUN COMMAND"

### Disable Telemetry
1. Open the app (again)
2. Click on the "TELEMETRY" button
3. Select "OK"

### That's all
You now have sucessfully disabled telemetry on your Oculus Quest. Have fun with your freed device.
