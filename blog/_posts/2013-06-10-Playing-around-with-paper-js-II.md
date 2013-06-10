---
layout: default
title:  Playing Around with Paper.js
published: true
---
Last week i posted about some experiments I did with [Paper.js][0]. Well my first approach is [this][1]. Some time ago, I was stunned
with [flat surface shader (FSS)][2] and decided to port the native js application to PaperScript. So far the differences are huge.
First of all, the work of [Matthew Wagerfield][3] is extremely clean, beautiful and easy to understand. Might be the [three.js][4] influence, I don't know. The thing is Matthew decided to write his own shader engine from the ground up, no libraries at all, just pure and clean JavaScript with some experimental features like Float32Array. The good thing is this small shader engine works with webgl, canvas and SVG and is a perfect introduction to advanced graphics on the web. But, I wasn't interested in just using the shader nor building an engine of my own. My overall goal was to learn a new technology through a framework I was already familiar and, without saying I'm proficient, I think I reach it.

My practical goal was to build an animatable mesh and the [FSS][2] was an excellent example, I didn't care too much porting it to [Paper.js][0]. The firs thing i noticed was paperjs was completely 2D, not a single glimpse of a z coordinate. The points are 2 values arrays (x,y), the paths are objects themselves, the output is HTML5 canvas only and the events are predefined. My approach was to create superobjects composed from the [Paper.js][0] primitives. [FSS][2] taught me not just graphics manipulation but Javascript rethorics too.

Next week i will be posting ideas and maybe some tutorial on HTML5 Canvas and [Paper.js][0]

[0]:http://paperjs.org
[1]:http://marcoslhc.github.io/paperjs-tutorials/
[2]:http://wagerfield.github.io/flat-surface-shader/
[3]:https://github.com/wagerfield/
[4]:http://threejs.org/