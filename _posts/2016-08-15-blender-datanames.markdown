---
layout: post
title:  "Blender script: How to change the object data name to the object name"
date:   2016-08-15 10:18:00
categories: blender
---

If you rename an object in blender, you likely didn't change the name of the object data.
There is a difference in the name of the object itself, and the name of the object data.
When you rename one, the other isn't automatically renamed. 

When you export your object to a `.obj` and the object has different names, it will put these names together during export. For instance, your object is named `Floor`, and the object data name is `Plane`.
When the object is exported, the mesh will have the name `FloorPlane`. If both names are equal, it will not duplicate the names. For example; the object name and data name are both `Floor`, the exported name will be `Floor`

Since I don't want to manually go over every object, I use this very small script that will change all the names to match the object name:

{% highlight python %}
import bpy

for obj in bpy.data.objects: #1
    obj.data.name = obj.name #2
{% endhighlight %}

This will loop over all the objects `(1)` in the scene and rename the data name to the object name `(2)`.