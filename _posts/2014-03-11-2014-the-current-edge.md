---
layout: post
title: "2014: The Current Edge"
modified: 2014-03-11 12:38:20 -0600
tags: [HTML5, CSS3]
image:
  feature: 
  credit: 
  creditlink: 
comments: true
share: true
---

#Moving into the Present...
# HTML5, CSS3, and ES5/Strict   <a name="html5-css3-es5"></a>

## HTML5 <a name="html5"></a>
Offline and Data storage

* Allows browsers (and through them web apps) to store data on the client machine
* This allows web apps to load quickly
* It also allows easier 'state' tracking on the client-side

Connectivity: Web Socket and Server Sent Events

* Opens up a "new" paradigm of client-server communication
* Allows servers to push new data to the client when it becomes available, rather than waiting for the client to request it.

File Access

* Easier file uploads
* Manipulation of data on the client machine

Semantics

* New and updated tags and attributes


<div contenteditable="true">
    This is an editable content box. Pure HTML5.
</div>

<input type="email" placeholder="bazinga@example.com" required >

~~~ html
        <input type="email" placeholder="bazinga@example.com" required>
        <div contenteditable="true">
            This is an editable content box.
        </div>
~~~ 

* Microdata

~~~ html
            <div itemscope itemtype="http://data-vocabulary.org/Person">  
              <img src="avatar.jpg" itemprop="photo">  
              My name is <span itemprop="name">Callum Kerr</span>, and I am a <span itemprop="title">developer</span> for  
              <a href="http://imageineagency.com" itemprop="affliation">Hot Pink, Ink</a>.  
              I live in  
              <span itemprop="address" itemscope  
                itemtype="http://data-vocabulary.org/Address">  
                <span itemprop="locality">Rapid City</span>,  
                <span itemprop="region">SD</span>  
              </span>  
            </div>  
~~~

Graphics

* Canvas
* WebGL
* SVG
* SMIL (Synchronized Multimedia Integration Language, pronounced "Smile")

Presentation

* CSS3 

Performance

* Making things faster

Nuts & Bolts

* Significant API improvements.
* Geolocation.
* History



## CSS3 <a name="css3"></a>

* Animations and Transforms
* Gradients, transparencies, multiple background images
* 3D Effects
* Web Fonts
* Flexboxes!



## ES5 <a name="es5"></a>

* Includes a bunch of technical bug fixes.
* Adds Array methods.
* More geeky stuff with dates and things.
* Adds JSON: JavaScript Object Notation (replaces XML)

