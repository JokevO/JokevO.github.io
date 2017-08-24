---
layout: post
title:  "Blender script: How to make sure that every face has maximum 4 edges"
date:   2016-08-14 10:18:00
categories: blender
---

When exporting an `.obj` object for use within Three.js, you will likely use the `OBJLoader.js` for importing the object.
One thing the OBJLoader does not support, are objects with n-gons.

In order for the object to correctly import, every face can have maximum 4 edges. I made a script that will automatically check if these faces are present and change them to quads/triangles.

{% highlight python %}
import bpy

for obj in bpy.data.objects: #1
	if obj.type == 'MESH': #2
		bpy.context.scene.objects.active = obj #3
		bpy.ops.object.mode_set(mode = 'EDIT') #4
		bpy.context.tool_settings.mesh_select_mode = (False, False, True) #5
		bpy.ops.mesh.select_all(action='DESELECT') #6
		bpy.ops.mesh.select_face_by_sides(number=4, type='GREATER') #7
		bpy.ops.mesh.quads_convert_to_tris() #8
		bpy.ops.mesh.tris_convert_to_quads() #9
		bpy.ops.object.mode_set(mode = 'OBJECT') #10
{% endhighlight %}

First, we loop over all the objects in the scene `(1)` and check if the object is a mesh `(2)`. When we have a mesh, we will make that mesh the currently active object `(3)`. 
We do this to make sure we have the right object selected when we are going into EDIT mode `(4)`. In EDIT mode, we make sure we are going to work with the faces `(5)`, and deselect all faces that would currently be selected `(6)`. 
After that, we search and select all the faces that have more than 4 edges `(7)`. We triangulate these faces `(8)`, and then attempt to convert these triangles into quads `(9)`.
Last but not least, before moving on and searching for the next mesh, we set the scene back into object mode `(10)`.