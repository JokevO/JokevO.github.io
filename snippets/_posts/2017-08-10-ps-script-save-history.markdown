---
layout: post
title:  "Photoshop script: resize and save file"
date:   2017-08-10 06:30:00
categories: photoshop
---

For my own personal project, I have been working quite a lot with photoshop.
To keep the repetitive tasks to a minimum, I tried to script most of them. One of these is resizing and then saving/overwriting the image as a png to some location. Here is one way to do that:

{% highlight javascript %}
function savePNG(saveFile) {  
    var saveOptions = new PNGSaveOptions();  
    saveOptions.compression = 9;  // (level of compression 0 .. 9       0 - without compression)
    saveOptions.interlaced = false;
    app.activeDocument.saveAs(File(saveFile), saveOptions, true, Extension.LOWERCASE);  
}

var savedState = app.activeDocument.activeHistoryState; //1
app.activeDocument.resizeImage(UnitValue(2000,"px"),null,null,ResampleMethod.AUTOMATIC); //2
savePNG("C:/image.png"); //3
app.activeDocument.activeHistoryState = savedState; //4
{% endhighlight %}

Before manipulating the image in any way, make sure to store the current history state of the image `(1)`. This way, you can always go back in history to that point. Then, resize the image to 2000 pixels in width `(2)`. Using this method, the aspect ratio will be used for calculating height. After that, the image will be saved to `C:/image.png` `(3)`. This line will call the savePNG function above, saving it as a png with the compression and interlaced options added. To end the script, set the image history (saved in `(1)`) to restore the image back to its original size`(4)`.