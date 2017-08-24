---
layout: post
title:  "C++: view bit pattern"
date:   2016-12-03 10:18:00
categories: c++
---
I was working on a hardware project, and I needed to be able to send a lot of data with only 12 bytes. Therefore when I needed to puzzle some bytes together, I opened up an [online c++ compiler](http://codepad.org/) and got to testing quickly.
In C++ you can import a library called `bitset`. It is useful when you want to print out your bitpattern and see the result when you are shifting bits. Here is an example:

{% highlight c++ %}
#include <iostream>
#include <bitset>

using namespace std;

int main()
{
  uint8_t number1 = 1;
  uint8_t part = number1 >> 4;
  int number2 = 35981;
  
  cout << bitset<8>(number1) << endl;
  cout << bitset<8>(part) << endl;
  cout << bitset<32>(number2) << endl;
}
{% endhighlight %}

This will output:
{% highlight c++%}
11111111
00001111
00000000000000001000110010001101
{% endhighlight %}