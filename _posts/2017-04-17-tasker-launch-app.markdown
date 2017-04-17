---
layout: post
title:  "Tasker: launch app when you plug in headphones"
date:   2017-04-17 09:18:00
categories: tasker android
---

Another [Tasker] post, I love how you can automate almost everything you usually have to do manually.
This is a very easy task, but I find it very useful. When I am at work, I listen to [Noisli].
I find this helps me keep my focus, but you can also do this with [Spotify] or any other app.
I listen to this on my phone, but when I have a meeting, I do take my phone with me.

Therefore I made a task that will launch [Noisli] when I plug in my headphones, and kill the app when I unplug them:
1. Go to the tab `TASKS` and add a new one, called `Launch Noisli`.
2. Add an action `App -> Launch App`, and select the app you want to open.
3. Press back button to confirm.
4. Add another task called `Kill Noisli`.
5. Add the action `App -> Kill App`, and select the app you want to close when you unplug your headphones.
6. In tab `PROFILES`, add a new profile `State -> Hardware -> Headset Plugged`. Press back button to confirm.
7. Link task `Launch Noisli`. This will launch the app when your headset is plugged in.
8. Long press `Launch Noisli` in the profile and press `Add Exit Task`.
9. Link `Kill Noisli` to the exit task and it will kill the app when you disconnect your headphones.

[Tasker]: https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm
[Noisli]: https://play.google.com/store/apps/details?id=com.noisli.noisli
[Spotify]: https://play.google.com/store/apps/details?id=com.spotify.music
