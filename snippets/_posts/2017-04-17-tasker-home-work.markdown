---
layout: post
title:  "Tasker: automate your android phone"
date:   2017-04-17 06:18:00
categories: tasker android
---

If there is one app I can definitely recommend when having an android phone, it is [Tasker]. This app is not free, but well worth the money. When you have to do something on your phone manually over and over, you can just automate it using the app.
It also does not use a lot of battery but will potentially save some.

One of the most simple things I do to save on battery, is to turn off wifi when I leave home, and turn it back on when at work and vice verca. Also, when I step outside I might want to get into the car and connect with it over Bluetooth. I would have to enable bluetooth when leaving home or work.

Here is how I automated it using [Tasker]:

I created a task that will turn on Wifi and turn off Bluetooth:
1. Open Tasker and in the tab `TASKS`, make a new task called `At Home/Work`. 
2. In this task add an action `Net -> WiFi`, and set `Set` to `on`. 
3. Press back button to confirm.
4. Add a new action `Net -> Bluetooth`, and `Set` to `off`.
5. Press back button again to confirm task.

Then I created a task that will do the oposite:
1. Open Tasker and make a new task called `Leaving Home/Work`. 
2. In this task add an action `Net -> WiFi`, and set `Set` to `off`. 
3. Press back button to confirm.
4. Add a new action `Net -> Bluetooth`, and `Set` to `on`.
5. Press back button again to confirm task.

Now we that we have the tasks ready, we just need to make them trigger at the right time.
I will be using location.

Trigger tasks:
1. Go to the tab `PROFILES` and add a new profile based on location.
2. Either fill in the right lat and lon, or longpress the map and it will put a marker there.
Adjust the radius to 100m and whether or not you want to use gps or just net. I only use `Net`.
3. Link your `At Home/Work` task to the profile. You see it is linked with `->` icon in profile. This indicates that the task will be triggered when you enter the profile location.
4. Long press the task in profiles and select `Add Exit Task` and select the `Leaving Home/Work` task. You will see it linked with the `<-` icon. This indicates the task that will be triggered when you exit that location.

[Tasker]: https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm