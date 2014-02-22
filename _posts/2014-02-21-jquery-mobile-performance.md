---
layout: post
title: "jQuery Mobile Performance Tips"
modified: 2014-02-21 16:03:53 -0700
tags: [jQuery Mobile, Performance]
image:
  feature:  jquery-mobile.jpg
  thumb:    jquery-mobile-thumb.jpg
  credit:   jquerymobile.com
  creditlink: http://jquerymobile.com/
comments:   true
share:      true
---

I recently attended a webinar from [Ralph Whitbeck](http://ralphwhitbeck.com/) and [AppendTo()](http://modernweb.com/webinars.php), "jQuery Mobile Perfomance Tips". Here's my notes. Some helpful tips for web apps or sites in general.

1. Use static content.
    -   Use static HTML
    -   Use static jQM (jQuery Mobile) pages.
    -   Use a backend language to generate HTML:
        -   DON'T use jQuery to generate the HTML.

    Mobile browsers still have performance issues in rendering JavaScript. As much as you can give the mobile browser pre-generated, do so.

2. Avoid DOM Manipulation. {#avoid-DOM-manipulation}

    jQuery's great where you need it, but excessive DOM manipulation will result in slow-to-render pages or '[jank](http://jankfree.org/)'.

3. Use Multi-Pages

    I.e. place as many pages as possible within the same HTML document. This will allow jQuery Mobile to load new pages without any new HTTP requests.

4. Group Common Pages together

    Place associated pages that are likely to be accessed in the same session together, as one multi-page HTML document.

5. Pre-load pages that are likely to be requested next

    So that when they are requested, they're already there, and load like a smooth, buttery, nut-brown ale. Comes in quick, goes down easy ;)

    * Use `data-ajax="false"` to load links to pages external to the current JQM site, when you are using reference anchors in the URL.

    For example:

~~~ html
        <a href="www.external-example.org/page#specificID">External Link</a>
        <!-- JQM will look for this page as a <div data-role="page"> within the current document, and fail -->

~~~

    Instead use:

~~~ html
        <a href="www.external-example.org/page#specificID" data-ajax="false">External Link</a>

~~~

6. Pre-render Widgets

    jQM and other frameworks will add a bunch of classes to certain widgets after page load. This [DOM Manipulation](#avoid-DOM-manipulation) slows down the render process. When you've built the page, you can load it in your browser, inspect the elements and take note of the classes that have been added automatically. Then add those classes inline to your HTML source. Boom! Instant performance benefit.

7. Combine and minify JavaScript and CSS

    But you already do this... right?

8. Make sprites where possible.

    Combining images together results in fewer HTTP requests. While this may not be practical in some situations, mobile's high latency means this can result in big load-time savings. [Ralph Whitbeck](@rwhitbeck) gave the example of the Speaker pages, each of 74 odd speakers requiring their own profile picture. That's a lot of http requests, when all of the pages are loaded in the same HTML document.

9. Eliminate cruft whereever you find it.

10. Use the local cache

    With the use of a `.appcache` file, and a `<html manifest="offline.appcache">` declaration. you can specify all the resources that the browser should download and cache locally (including resources for pages that haven't been accessed yet). Using this technique, the user only needs to visit your page once, and with a small hit on their initial load time, the entire app will be available to view, even over an intermittent (or non-existent) internet connection. More information on the HTML5 local cache is available at [HTML5Rocks](http://www.html5rocks.com/en/tutorials/appcache/beginner/).

11. Polish

    For extra style points on iOS, specify apple touch icons, to show up if a user bookmarks the web app to their home screen, and an iphone splash screen, that displays while the app loads.

    Apple touch icons:

    ~~~ html
        <link rel="apple-touch-icon" href="touch-icon-iphone.png" />
        <link rel="apple-touch-icon" sizes="76x76" href="touch-icon-ipad.png" />
        <link rel="apple-touch-icon" sizes="120x120" href="touch-icon-iphone-retina.png" />
        <link rel="apple-touch-icon" sizes="152x152" href="touch-icon-ipad-retina.png" />
    ~~~

    iPhone Splash Screen:

    ~~~ html
        <link rel="apple-touch-startup-image" href="/startup.png">
    ~~~

    Additional resources:

    [ModernWeb.com](http://modernweb.com/)

    [Apple Developer Network](https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html)

