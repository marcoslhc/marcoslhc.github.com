---
layout: posts
title:  Playing Around with Paper.js (&amp; III)
published: true
---

In my [last post][0] i talked about the [Flat Surface Shader][1] and my implementation in [Paperjs][2]. One thing I regretted in Paperjs is the PaperScript implementation. IMHO is not a separate Script but simple a wrapper that just prevents polluted code providing a separate scope and provides a convenient form of vector operations (\+,\-,\*,/,%): `vectorA = vectorB + vectorC` instead of `vectorA.add(vectorB).add(vectorC)`. The rationale of this design according with the authors is that you can have multiple scripts in one page sharing the paper.js library, each script with its own context and scope.

Thats pretty cool for demo and tutorials, but when you want to write extensive code and you want it to be reusable, understandable or just readable, even debbugable; the PaperScript approach indefectibly fails. You cannot expose objects across different scripts and since paper.js loads the PaperScript code and excecute it, the debbuging is, at least, torture. But the good part is, like I said before, PaperScript is just JavaScript, so if you don't mind accesing all library's objects with the `paper` prefix, manually manage the scope and projects within and using `Math` instead of point and vector operators, you can load your code like any other script. If you want more information on how to treat Paperjs scripts like regular javascript read [Using JavaScript Directly][3] in the [Paperjs Tutorials][4].

One of the things i talked in the las pyost, was the way the [FSS source code][1] was written: Modular, simple and functional enough, and I though that an AMD style architecture would be a good thing to use there and after the functional requirement (move the mesh) I
decided to try to modularize the code using RequireJS and the result can be seen here: [http://github.com/marcoslhc/paperjs-tutorials][5].

The module definition was the easiest part, just wrap the objects constructor and prototype enhancements in a `define()` function. Then i have to include the library; since paperjs is not written in AMD Style i used the shim configuration in RequireJS:

    
    requirejs.config({
      baseUrl:"js/",
      paths:{
        'paper':'paperjs-nightly/lib/paper'
      },
      shim:{
        'paper':{
          exports: 'paper'
        }
      }
    });
    
when the library is required  the paper object is added to the Global Scope, so two thing to care of, you have to required it with
other name than `paper` in the example below we use `s` and then call it with   `paper`.


    require(['paper','Plane'],function(s,Plane){
      var canvas = document.getElementById('tutorial')
      paper.setup(canvas);
      var geometry = new Plane();
      var now, start = Date.now();
      paper.view.draw();
      paper.view.onFrame = function(){
        now = Date.now() - start;
        geometry.update(now);
        
      }
    });

You're invited to [read the code][5] :)

[0]:/blog/2013/06/10/Playing-around-with-paper-js-II.html
[1]:http://wagerfield.github.io/flat-surface-shader/
[2]:http://paperjs.org
[3]:http://paperjs.org/tutorials/getting-started/using-javascript-directly/
[4]:http://paperjs.org/tutorials/
[5]:http://github.com/marcoslhc/paperjs-tutorials