---
title: Play Spotify and Discord on Oculus Quest in 2022
layout: post
description: This tutorial will show you how to play Spotify songs or talk to your friends on Discord while playing VR games
tags: post oculus oculus quest quest spotify discord facebook tutorial
minute: 2
---

## Video Tutorial
If you prefer a video tutorial you can watch [this one](https://www.youtube.com/watch?v=aMnHgz2Zo3E) I made.

## Intro
Hello and welcome, today I’m going to show you how to enable background audio recording and playback on the Oculus Quest.

## Enable Developer mode
First you will need to enable Developer mode on your Quest, most of you probably already have it enabled, you can follow [this tutorial to enable developer mode](https://developer.oculus.com/documentation/native/android/mobile-device-setup/)

## Download Oculess
Next you will need to [download an app that I have written called Oculess](https://github.com/basti564/Oculess/releases/tag/v1.3.3), if you already have it installed you’re probably on an older version of it that doesn’t have the background audio feature so you still have to download this update. All you need to do is save the .apk file from GitHub on your desktop so that you can access it later. 

## Download Discord or Spotify
Then we need to get a copy of the app you want to use in the background, for example [Discord](https://m.apkpure.com/discord-chat-talk-hangout/com.discord/download) or [Spotify](https://m.apkpure.com/spotify-music-i/com.spotify.music/download). The links are from Apkpure, but it doesn’t really matter from where you get yours.

## Sideloading the APK
There are many ways to install the apps we have downloaded. I’m going to show you how to install the apps via SideQuest since it’s the easiest way and you probably already have it setup, but if you are using a PC you can also install the downloaded apps directly via ADB, or if you are using an android phone you can use [Bugjaeger](https://play.google.com/store/apps/details?id=eu.sisik.hackendebug&hl=en&gl=US) with an OTG cable to install them.

If you already know how to sideload an APK to the Quest, just download the APK from step 1.
1. Click this icon in SideQuest 

![Install APK from folder](/assets/images/posts/install.PNG)
2. Select the APK files you have downloaded
3. Wait for the upload to finish

## Activating it
After you have installed all APKs onto the Quest you first need to activate Oculess. To do that, put on your headset and open the Oculess app. In it click on the “remove accounts” button and remove all the accounts, typically 2, from your Quest. This is only temporary and they will return in a few minutes.
Take off the Quest and head back to SideQuest "Run ADB commands">"Custom ADB command" to enter the following command `adb shell dpm set-device-owner com.bos.oculess/.DevAdminReceiver`.

## Enable Background Playback
Oculess is now able to enable background playback for other apps. So open Spotify (or any other audio app you like), start a song, close Spotify and head back to Oculess, which will now allow you to reenable background playback, by clicking on the. “Enable Background Audio for Installed Apps” Button. This will stay enabled as long as you do not restart the Headset.