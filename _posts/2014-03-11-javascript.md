---
layout: post
title: "Javascript"
modified: 2014-03-11 12:43:03 -0600
tags: [Javascript, AJAX ]
image:
  feature: 
  credit: 
  creditlink: 
comments: true
share: true
---

## jQuery and other Javascript Frameworks and Libraries <a name="jquery"></a>

Javascript frameworks are collections of useful methods and functions (hence: libraries). They abstract some of the nitty-gritty functions that we use when programming web sites. They also standardise functions to work cross-platform.

For example:

~~~ javascript
    $('.title').fadeIn('slow');
~~~ 

Compared to:

~~~ javascript
    animate: function( prop, speed, easing, callback ) {
        var empty = jQuery.isEmptyObject( prop ),
            optall = jQuery.speed( speed, easing, callback ),
            doAnimation = function() {
                // Operate on a copy of prop so per-property easing won't be lost
                var anim = Animation( this, jQuery.extend( {}, prop ), optall );

                // Empty animations resolve immediately
                if ( empty ) {
                    anim.stop( true );
                }
            };

        return empty || optall.queue === false ?
            this.each( doAnimation ) :
            this.queue( optall.queue, doAnimation );
    }
~~~ 

There are **loads** of different frameworks, and most of them are great. A lot of them do the same things. jQuery is a great one, providing a hugely solid base foundation for web programming.

# AJAX: Asynchronous JavaScript and XML <a name="ajax"></a>

AJAX is a dominant technology in current web development. Prior to AJAX, any state-changing interaction with the web page required a full page reload in the browser. And this was inefficient. In most cases, this results in a lot of the same data being re-sent to the browser on each user interaction. 

The innovation of AJAX is to allow the application to only load the data that is needed for the update of the application. When the user makes a change in the page that requires more data, a Javascript function is fired from behind-the-scenes, to ask the server for _just the information that is needed_. Previously, whenever the user clicked on a link on a page, the browser would reload an entire HTML page, with headers, all the page navigation, and then would need to cache-check all the images and other resources used on the page. All of this activity adds up, although we have become so used to it from using sites built with the previous paradigm.

This is the key to creating responsive web applications, that are able to keep a user's focus over a long series of interactions. At a neurological level, humans have a "distraction threshold" that is approximately 100 ms. That's a tenth of a second. We may not be conscious of this, and when trying to accomplish a task, we focus really hard and try to overcome this distraction, but on a physical level, we cannot respond in as focussed a manner when an application exceeds this distraction threshold. 