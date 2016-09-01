---
layout: post
title:  "Terminal: check for valid json"
date:   2016-08-18 10:18:00
categories: terminal ruby npm bash
---

When I manually want to check for a valid json, I have always used [jsonlint]. I discovered that jsonlint has an npm and ruby package.
You can find the plugin here: [npm] or [ruby].
You can either install it with `npm install jsonlint -g` (for npm) or `gem install jsonlint` (for ruby).

You can now use it in terminal like this `jsonlint filepath.json`. This will output nothing if it was successful or it will print where it went wrong.

Or if you want to use it in a script that will check for the validity, here is an example:
{% highlight bash %}
#!/bin/bash

jsonlint $JSON_TO_VALIDATE_PATH

#Check if json is valid
if [ $? != 0 ]
then
    echo JSON NOT VALID
    exit 1
else
    echo JSON IS VALID
fi
{% endhighlight %}

[jsonlint]:    http://jsonlint.com/
[npm]: https://github.com/zaach/jsonlint
[ruby]: https://github.com/PagerDuty/jsonlint