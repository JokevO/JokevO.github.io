---
layout: post
title:  "Tasker: weather report"
date:   2017-04-23 06:30:00
categories: tasker android
---

Instead of using a weather app, I made a [Tasker] task that will give me a notification with a short weather description twice a day. In the morning the weather of the current day, and in the evening with the weather for the next day.

Here is how I created the task for the current day.
I used the [Wunderground] api, I signed up for an api key so I can get that data.
1. Create a new task called `Weather Today`.
2. Add an action `Net -> HTTP Get`.
3. Set Server:Port to `api.wunderground.com`.
3. Set Path to `api/API_KEY/conditions/forecast/q/Belgium/ANTWERP.json`. replace the `API_KEY` with the key you created with [Wunderground]. Replace `Belgium` with the country you live in, and `ANTWERP` with your current city.
4. Go back to confirm.

In orde to test if this works correctly, you can create an `Alert -> Flash` and set `%HTTPD` as text. Press Play. If there is output, you know the call is correct.

5. Add a new action `Code -> JavaScriptlet` and add this code `var weather = JSON.parse(global('HTTPD')).forecast.txt_forecast.forecastday[0].fcttext_metric;`.
6. Add a new action `Code -> JavaScriptlet` and add this code `var title = JSON.parse(global('HTTPD')).forecast.txt_forecast.forecastday[0].title;`.
7. Add a new action `Code -> JavaScriptlet` and add this code `var icon = JSON.parse(global('HTTPD')).forecast.txt_forecast.forecastday[0].icon_url;`.
8. Add a new action `Code -> JavaScriptlet` and add this code `var city =JSON.parse(global('HTTPD')).current_observation.display_location.city;`.
9. I used [AutoNotification] to create the actual notification. When the app is installed, create a new action `Plugin -> AutoNotification`.
10. Under Texts, as Title and Title Expanded, set `%title`.
11. Under Texts, as Text and Text Expanded, set `%weather`.
12. Under Texts, as SubText, set `%city`.
13. Under Icons and Images, set `%icon`.
14. Press back to confirm.

Now the task is complete, we need to create a profile that will trigger the task when we want.
15. Go to tab `PROFILES` and create a new profile `Time` and set the time you would like the notification.
16. Choose task `Weather Today`.
17. Press back to confirm.

Here is an example notification:
![alt text][Example]

[Tasker]: https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm
[Wunderground]: http://api.wunderground.com
[AutoNotification]: https://play.google.com/store/apps/details?id=com.joaomgcd.autonotification
[Example]: https://raw.github.com/JokevO/JokevO.github.io/master/assets/images/weatherscreen.png "Example"