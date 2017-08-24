---
layout: post
title:  "Ruby: manipulate json"
date:   2017-08-10 06:30:00
categories: json ruby
---

I started a project, which used an existing json file full of data.
Because not all data was necessary, I decided to clean it up and rename some keywords.
Instead of doing that manually, I created a ruby script.

Here is an example of the input and the prefered output json:
{% highlight javascript %}
// json we start with
[
 {
   "Country Name": "Christmas Island",
   "ISO2": "CX",
   "ISO3": "CXR",
   "Continent": "Asia",
   "Capital": "Flying Fish Cove"
 },
 {
   "Country Name": "Cocos Islands",
   "ISO2": "CC",
   "ISO3": "CCK",
   "Continent": "Asia",
   "Capital": "West Island"
 }
]
{% endhighlight %}

{% highlight javascript %}
// the output we are going for
[
 {
   "name": "Christmas Island",
   "iso2": "CX",
   "continent": "Asia",
   "capital": "Flying Fish Cove"
 },
 {
   "name": "Cocos Islands",
   "iso2": "CC",
   "continent": "Asia",
   "capital": "West Island"
 }
]
{% endhighlight %}

This is the script used for modifying this json file:
{% highlight ruby %}
require 'json'

file = File.read('./input.json') #1
data = JSON.parse(file) #2

output = [] #3

data.each do |child| #4
  output.push({ #5
    :name => child['Country Name'],
    :iso2 => child['ISO2'],
    :continent => child['Continent'],
    :capital => child['Capital']
  })
end

#save output to other json file
File.open('./output.json', 'w') do |f| #6
  f.write(JSON.pretty_generate(output)) #7
end
{% endhighlight %}

First, we read the input file `(1)` and parse it `(2)`. We create an empty array that we will use for storing our new json `(3)`. Now we loop over each existing json entry `(4)`, create a new object, and fill that object with the information we want to keep `(5)`. Once we have looped over all the entries, we are going to save the file as `output.json`. To do this, open that file as writable `(6)`. If the file does not exist yet, it will automatically be created. For extra readability, we can pretty print the json using the `pretty_generate` function `(7)`. This will ouput the file as listed above.

