---
layout: post
title:  "Photoshop script: scripting listener"
date:   2017-10-18 06:30:00
categories: photoshop
---
When you are scripting in photoshop, you will notice not all operations you use in photoshop are found in the [scripting reference]. These operations can be used through the action manager (if the action is recordable).

To help you with the actions, you can install a plugin called [ScriptingListener]. This plugin will record every action you do in photoshop and output them in two txt files. These files will be saved on your desktop and are called `ScriptingListenerJS.log` and `ScriptingListenerVB.log`. `ScriptingListenerJS.log` contains all recorded actions translated to javascript. `ScriptingListenerVB.log` contains the same but translated to visual basic script.

Every action in these files are seperated by `// ============`. When you do a selection by color range for example, this action can be found in `ScriptingListenerJS.log` and looks like this:

{% highlight javascript %}
var idClrR = charIDToTypeID( "ClrR" );
    var desc69 = new ActionDescriptor();
    var idFzns = charIDToTypeID( "Fzns" );
    desc69.putInteger( idFzns, 0 );
    var idMnm = charIDToTypeID( "Mnm " );
        var desc70 = new ActionDescriptor();
        var idLmnc = charIDToTypeID( "Lmnc" );
        desc70.putDouble( idLmnc, 51.330000 );
        var idA = charIDToTypeID( "A   " );
        desc70.putDouble( idA, 2.330000 );
        var idB = charIDToTypeID( "B   " );
        desc70.putDouble( idB, -61.690000 );
    var idLbCl = charIDToTypeID( "LbCl" );
    desc69.putObject( idMnm, idLbCl, desc70 );
    var idMxm = charIDToTypeID( "Mxm " );
        var desc71 = new ActionDescriptor();
        var idLmnc = charIDToTypeID( "Lmnc" );
        desc71.putDouble( idLmnc, 51.330000 );
        var idA = charIDToTypeID( "A   " );
        desc71.putDouble( idA, 2.330000 );
        var idB = charIDToTypeID( "B   " );
        desc71.putDouble( idB, -61.690000 );
    var idLbCl = charIDToTypeID( "LbCl" );
    desc69.putObject( idMxm, idLbCl, desc71 );
    var idcolorModel = stringIDToTypeID( "colorModel" );
    desc69.putInteger( idcolorModel, 0 );
executeAction( idClrR, desc69, DialogModes.NO );
{% endhighlight %}

You can then use this code directly in your other photoshop js scripts.


[scripting reference]: http://www.adobe.com/content/dam/acom/en/devnet/photoshop/pdfs/photoshop-cc-javascript-ref-2015.pdf
[ScriptingListener]: https://helpx.adobe.com/photoshop/kb/downloadable-plugins-and-content.html#ScriptingListenerplugin