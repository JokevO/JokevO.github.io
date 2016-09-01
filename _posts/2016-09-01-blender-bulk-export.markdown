---
layout: post
title:  "Blender Script: bulk export objects"
date:   2016-09-01 10:18:00
categories: blender python
---

When working with blender, something you will most likely do is export your object.
If there are a lot of these objects, and you want to export your meshes into seperate .obj files, it can be a very tedious job.
The script below is one I use to make this as fast and easy as possible:

{% highlight python %}
import bpy

# -----
# optional if you want to export a folder but the folder might not exist yet
import os

directory = bpy.path.abspath("//exports/")
if not os.path.exists(directory):
    os.makedirs(directory)
# -----

for obj in bpy.data.objects: #1
	if obj.type == 'MESH': #2
		bpy.ops.object.select_all(action='DESELECT') #3
		obj.select = True #4
		file_path = bpy.path.abspath("//exports/" + obj.name + ".obj") #5
		bpy.ops.export_scene.obj(filepath=file_path, use_selection=True, use_materials=False, global_scale=1, use_smooth_groups=True, use_normals=True, use_uvs=True) #6
{% endhighlight %}

First, we loop over all the objects in the scene `(1)` and check if the object is a mesh `(2)`.
If we found a mesh, we deselect everything in the scene `(3)`, and select the mesh we want to export `(4)`.

Then we define where the objects will be saved `(5)`. In this example the objects will be saved in a folder named `exports` (optionally add the folder).
The `bpy.path.abspath` will return the absolute path and the `//` is an identifier in blender that points to the current blend file.
We add the data name of the object to it, along with the `.obj` extension. If the blend file is not saved, the absolute path will be empty.

Last but not least, we export the obj with the settings we want `(6)`. In this example, only the selection and no materials will be exported.