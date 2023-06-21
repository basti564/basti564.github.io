---
title: Using the Oculus Quest without an Account
layout: post
description: This tutorial will show you how to log out from your Oculus/Facebook account on your Oculus Quest
tags: post oculus quest oculess sideloading tutorial
---

## Please read before you continue
This tutorial has been tested on multiple Quest 1 and 2 devices, but there is always the chance that something might not work on your device and that something will break. If you just want to use your Quest 2 without a Facebook account and are okay with using an unmerged Oculus/Oculus developer account follow this [Video Tutorial](https://www.youtube.com/watch?v=5cyijb7CJZU), which has *no* side effects. If you don't have an Oculus account or don't want *any* side effects consider just [disabeling Telemetry](/Disable-Telemetry/).

I'd like to thank [u/fisk47](https://www.reddit.com/user/fisk47) and [u/doctor_blob](https://www.reddit.com/user/doctor_blob) for testing this on their Quests.

##### What does work?
- Hand tracking
- PCVR via Oculus Link, Airlink or ALVR
- Using sideloaded apps and sideloading apps still works

##### What doesn't work?
- Oculus Store
- Launching Oculus Store apps through built-in launcher
- Most apps downloaded through the Oculus Store because of entitlement errors (including Virtual Desktop :/)
- Facebook's social (media) features
- The built-in casting options
- Oculus Browser
- Oculus TV

##### What can I use instead?
- Launching Oculus Store apps: [Quest App Launcher](https://github.com/tverona1/QuestAppLauncher)
- Virtual Desktop: [ALVR](https://github.com/alvr-org/ALVR) or [VRidge](https://vridgequest.riftcat.com/index.html)
- Casting: Sidequest includes an easy-to-use interface for scrcpy and wireless ADB
- For browsing and "TV": [Firefox Reality](https://github.com/MozillaReality/FirefoxReality)

##### Positive side effects
- Disables *some* Facebook telemetry
- The [piracy kill switch](https://www.reddit.com/r/OculusQuest/comments/dnuxfs/just_a_heads_up_that_the_latest_quest_90_update/) won't work anymore

# Tutorial
### Setting up the Quest 2 with an Oculus/Oculus developer account instead of a Facebook account (optional)
This step is optional and the tutorial will work with a Facebook account, but you can follow this [Video Tutorial](https://www.youtube.com/watch?v=5cyijb7CJZU) by "No Borscht For You" (original tutorial by [u/Tiger-Hobbes](https://www.reddit.com/r/OculusQuest/comments/jd6cfi/the_quest_2_has_allegedly_successfully_been_rooted/g9617l2?utm_source=share&utm_medium=web2x&context=3)) to set up your Quest 2 with an unmerged Oculus developer account instead.
*Maybe that's all you have been looking for, as just using an Oculus account doesn't have the side effects of this method (except nonfunctional Facebook social features). Note however that this might cease to work in 2022-2023, when (if) Facebook is going to force existing unmerged accounts to merge.*

### Sideloading the APK
If you already know how to sideload an APK to the Quest, just download the APK from step 1.
1. Download the Oculess.apk from [here](https://github.com/basti564/Oculess/releases)
2. Follow this [Video Guide](https://youtu.be/RoIXxIfRNTw?t=125) by "Virtual Reality Oasis"
3. Click this icon in Sidequest 

![Install APK from folder](/assets/images/posts/install.PNG)
4. Select the APK file you have downloaded in step 1
5. Wait for the upload to finish

### Logging out
1. Put on your Quest headset
2. Select the "Apps" tab
3. In the top right, scroll down and select "Unknown Sources" from the drop-down menu
4. Open the "Oculess" app (com.bos.oculess)
5. Click the "DISABLE COMPANION" Button
6. Choose "Companion Server" from the List
7. Click "Deactivate this device admin app" 
8. Restart your Quest

### Logging back in
1. Check in the "Oculess" app if the Companion Server is started
2. If it isn't click on the "ENABLE COMPANION", select "Companion Server" from the List and click "Activate this device admin app"
3. Check that your Quest is on the same network as your phone
4. Open the "Oculus" app on your phone
5. Go to the "Settings" tab
6. Click on your Quest and wait for your Quest to connect
7. Restart your Quest


The title image background was made by [kyu3](https://kyu3.blog.jp/profile.html) under the Creative Commons Licence (CC - BY - SA)
