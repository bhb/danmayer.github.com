---
layout: post
title: "Mobile Development and My Recommendation for PhoneGap"
category:
tags: []
---
{% include JB/setup %}
In the last month or so I have been exploring mobile development. I wrote basic native Android and iPhone apps. I also build cross platform apps using Rhodes, Titanium, and PhoneGap. I thought it would be good to share my thoughts and experiences on the mobile dev space.<br />If you want full control and are doing a lot of local heavy processing (CPU bound) native is the way to go. I program to the web data without access I don't do much interesting. When the whole app basically relies on live data I feel javascript, HTML, and CSS is the way to go. Not only am I already familiar with it, but basically the app can share code with the mobile site. Also, using JS, HTML, and CSS gives the most flexibility in terms of supporting multiple devices. Since I wasn't using anything specific to a single mobile device or really pushing the hardware, I quickly moved away from fully native apps. It wasn't worth the time and extra effort to write nearly the same app in Java, Objective C, and whatever else. Game developers, and those doing a bunch with video, photos, etc are probably most interested in native apps and probably won't be as interested in other options.<br />This lead me to explore [Rhodes](http://rhomobile.com/products/rhodes/), [Titanium](http://www.appcelerator.com/), and [PhoneGap](http://phonegap.com) as alternatives to purely native apps. All of which let you leverage HTML and CSS for building a UI.<br />Rhodes lets you write code in Ruby using a MVC framework. You leverage html (erb/haml) views using a Ruby back end to make remote requests, interact with a DB, and interact with native phone components. It is a cool framework, and obviously since it is Ruby, I enjoyed writing the code. However, it obscured the actual process of making an app for a device a bit much for my comfort. If something went wrong anywhere in the stack or if you wanted to break out of the Rhodes way to do something native on a platform it was difficult to do. It tries to manage the entire app development end to end hiding any per device customizations away from you. Since I wanted to be able to use some existing libraries for Android and iPhones, this limitation was a dealbreaker.<br />Titanium and PhoneGap use the same basic approach as each other providing a javascript library, which interfaces with native code for each device. You write an app in JS/HTML/CSS and make calls to the JS library to interact with native elements like the accelerometer, GPS, buttons, etc. I think it's a big win to be able to write most of the app in familiar web languages basically utilizing Ajax and local storage to give a nice mobile experience. Getting up and running on either Titanium or PhoneGap was painless. Again, in the end I wanted more control over some native components which caused me to choose PhoneGap over Titanium. While the concept is the same for both of these products, their approach is very different.<br />Titanium is a bit more all or nothing of an approach, you develop in Titanium's little world and it is best to not go out ofit. PhoneGap takes a extremely lightweight and minimalist approach to getting your project running on each device. It gives you basically the bare necessities and gets out of your way. PhoneGap doesn't try to configure the build environment and it doesn't manage simulators. To create a app with PhoneGap for any mobile platform you point to the same web directory (HTML, CSS, JS, and images), then generate a native app for the device. At that point you have the same native app project you would have if you were to start from scratch but you have a few nice libraries and code started for you. If you don't like the way PhoneGap does something, that is fine delete it, override it, extend it. You need to do something native PhoneGap doesn't support add your own JS handlers and interact with new or existing native code. I needed to allow for FaceBook connect login on Android, which PhoneGap doesn't support no problem. FaceBook maintains a Android SDK, which I imported into my PhoneGap project and added JS handlers which call to the FaceBook Android native code. There is a bug in Androids SSL cert verification for WebKit that was causing errors for HTTPS access, drop into java override the SSL Cert verification and fixed that. This would be difficult to do with Rhodes or Titanium because they don't allow you easily write and interact with your own native code. The project has to work only through the API provided to you to stay cross compatible. Which is great in some ways, but very limiting if you want to break out and just tweak a few little things.<br />I have been extremely happy working with PhoneGap, it rocks. It lets you build a native mobile app as a locally cached and privileged mobile website. You can leverage existing mobile site code for the native app. It will still be better than a pure website experience. It lets you piggyback on skill web developers already have. It is a great way to make use of HTML5  local DBs, local data, and HTML templates. It encourages you follow best practices for building a mobile site that works offline and requests only minimal JSON so it can fast over slow internet. <br />Before building an app with PhoneGap I recommend building a mobile site. Learn about best practices for the mobile web. If you are new to developing sites for mobile, I highly recommend following the recommendations from [Yehuda Katz on building great mobile sites](http://www.engineyard.com/video/12678746). He discusses some things specific to Rails 3, but mostly just good JS practices.<br />In many ways when building a PhoneGap app you are just building a mobile website. You have access to utilizing some native things that you can't with pure HTML/CSS. Local storage is a good example, it is supported by HTML5, but the earlier Android webkit didn't support it. Using PhoneGap you have local storage on old devices and it can use standard HTML5 local storage on newer devices.<br />Last but not least, PhoneGap has a great [active community](http://www.phonegap.com/community). Drop into #phonegap on freenode and people are always around to help out. The mailing list has a constant flow of questions and answers. While [PhoneGap docs](http://www.phonegap.com/docs) are a little out of date, there are people actively working on improving them. There are many example applications and open code on github to check out how to use PhoneGap. Also, the code is small and simple enough it is a great project to get involved in and give back. After working with it awhile, you will start to understand the internals and could help contribute patches, features, and plugins to the community. 