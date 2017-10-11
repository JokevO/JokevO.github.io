---
layout: post
title:  "Photoshop script: save image in pieces"
date:   2017-10-11 06:30:00
categories: photoshop
---
For my personal project, I started with a map of the world in photoshop. This map was 16384x8192. I exported the map at about half the scale to use in unreal. When I wanted to build the project on my phone, I bumped into an issue with it. My phone could only load images that were maximum 2048x2048px.

To export the map at 2048x2048 would lose too much of the detail. What I did instead, I split up the map (and globe to put the map on) in eight pieces. Now I do iterate on the map quite a lot and it would be a hassle to actually keep seperate photshop files for every piece of the map.

Instead, I wrote a script that will split the map for me, and save the pieces to the correct location. Here is how I did it:

{% highlight javascript %}
function savePNG(saveFile) {  //1
    var saveOptions = new PNGSaveOptions();  
    saveOptions.compression = 9;  // (level of compression 0 .. 9       0 - without compression)
    saveOptions.interlaced = false;
    app.activeDocument.saveAs(File(saveFile), saveOptions, true, Extension.LOWERCASE);  
}

var numberOfPieciesHorizontal = 4;
var numberOfPiecesVertical = 2;

var docwidth = app.activeDocument.width; //2
var docheight = app.activeDocument.height; //2
var sizeHorizontal = docwidth / numberOfPieciesHorizontal; //3
var sizeVertical = docheight / numberOfPiecesVertical; //3

for (var i = 0; i < numberOfPieciesHorizontal; ++i) { //4
  for (var j = 0; j < numberOfPiecesVertical; ++j) { //5
    // array is left, top, right, bottom
    app.activeDocument.selection.select(
        Array (
            Array(i * sizeHorizontal, j * sizeVertical),
            Array(i * sizeHorizontal, j * sizeVertical + sizeVertical),
            Array(i * sizeHorizontal + sizeHorizontal, j * sizeVertical + sizeVertical),
            Array(i* sizeHorizontal + sizeHorizontal, j * sizeVertical)
        ), SelectionType.REPLACE, 0, false); //6
    
    // crop
    var savedStateCrop = app.activeDocument.activeHistoryState; //7
    executeAction(charIDToTypeID('Crop'), new ActionDescriptor(), DialogModes.NO); //8

    // save
    savePNG("C:/map" + i + "_" + j + ".png"); //9
    app.activeDocument.activeHistoryState = savedStateCrop; //10
  }
}
{% endhighlight %}

To start, we get the current height and width of the document `(2)`. Depending on how many pieces, we calculate the width and height of each piece `(3)`. After that, we loop over all the horizontal pieces we will create `(4)`, and immediatly go over the vertical ones `(5)`. Now that we know which piece we are currently trying to export, we create a selection of that specific piece `(6)`. We remember the current state of the document `(7)`, crop the piece `(8)` and save it to the correct location `(9)`. We save using the function we have used in other scripts before `(1)`. Last but not least we restore the state to before the crop happend and do `(6 - 10)` over again until all pieces are exported.