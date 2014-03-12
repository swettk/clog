---
layout: post
title: "Clients, Servers, and other web hardware"
modified: 2014-03-05 18:13:00 -0700
tags: [Clients,Servers,Web Technology]
image:
  feature: 
  credit: 
  creditlink: 
comments: true
share: true
series: "The Modern Web"
---
## (aka: Welcome to the Internet!)

## Browsers (Clients) <a name="browsers"></a>
In general, most experiences of "The Internet" are experienced through a browser.

To initiate the experience, the browser sends a **HTTP Request** in response to some user interaction. 

~~~ html
        GET /path/file.html HTTP/1.0
        From: someuser@example.com
        User-Agent: Mozilla/5.0 (iPad; U; CPU OS 3_2_1 like Mac OS X; en-us) /
                    AppleWebKit/531.21.10 (KHTML, like Gecko) Mobile/7B405
~~~

This request is sent first to a Domain Name Server (DNS) that looks up the IP address of the requested address (www.example.com), figures out the quickest route to that box, and a **socket** is opened up between the client and the server. There are many other **Headers** that are (can be) sent with the file, some of which can be quite useful for analytical or responsive purposes (the User Agent, for example, that tells us which browser the request is coming from.)

When the server receives and validates the request, it will respond with something like the following, assuming that the request is ok, and the server has a file to return from the specified path.

~~~ html
        HTTP/1.0 200 OK
        Date: Fri, 31 Dec 1999 23:59:59 GMT
        Content-Type: text/html
        Content-Length: 1354

        <html>
        <body>
        <h1>Happy New Millennium!</h1>
        (more file contents)
          .
          .
          .
        </body>
        </html>     
~~~ 

After sending the response, the server closes the socket. Again, there are many headers that can be set for the response, of particular use in **Cache Control**, among other things.

## HTML, CSS and ECMAScript <a name="html-css-ecmascript"></a>

**HTML** is responsible for the *structure* of a webpage, and is used by the browser's parsing engine to generate the DOM (Document Object Model). In the beginning, HTML served mainly to transmit scientific documents, for which it was well suited. However, it was designed in a time with no conception of a "web application" or the myriad of uses that we put it to today. As such, it is an unwieldy "language" to "program".

~~~ html
        <!DOCTYPE html>
        <html>
            <head>
                <title>The Modern Web</title>
                <meta charset="utf-8">
                <link rel="stylesheet" href="style.css">

                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <meta name="description" content="An Overview of the Modern Web">
                <meta name="author" content="Callum Kerr">

                <link href="assets/css/bootstrap.css" rel="stylesheet">
                <script src="js/main.min.js"></script>
            </head>
            <body>
                <!-- this is an HTML comment -->

                    HTML Content goes here...

            </body>
        </html>
~~~ 

**CSS** is responsible for the *layout* and *appearance* or *presentation* of the page.

~~~ css
      body {
        padding-top: 20px;
        padding-bottom: 60px;
      }

        #container {
            width: 60%;
            margin:auto;
            font-family: 'futura-pt';
            display: none;
        }

        .wf-active #container {
            display: block;
        }

        .wf-active #loading {
            display: none;
        }
~~~ 



**JavaScript** (officially known as ECMAScript) is responsible for the *behaviour* of the page.

~~~ javascript
        $("a.clickMe").on("click", function() {
            //display a message to the user
            alert("You just clicked a link!\nPrepare to be teleported to another part of the internet!");
        });
~~~

<a href="http://www.google.com" class="clickMe">Click Me!</a>

### The DOM (Document Object Model)             <a name="dom"></a>
As a browser parses an HTML or xHTML document it creates the Document Object Model, which looks something like this:

<pre><code>
        |
        |--- ( HEAD )
        |       |
        |       |------- ( TITLE )
        |       |   
        |       |------- ( STYLESHEET )
        |       |   
        |       |------- ( SCRIPT )
        |       |
        |       |------- ( SCRIPT )
        |
        |--- ( BODY )
                |
                |------- ( DIV."container" )
                |               |
                |               |------------- ( DIV."header")
                |               |                   |
                |               |                   |---------- ( UL."navigation" )
                |               |                                  |
                |               |                                  |-------- ( A )
                |               |                                  |           |--------  text 
                |               |                                  |
                |               |                                  |-------- ( A )
                |               |                                              |--------  text 
                |               |------------- ( DIV."main")
                |                                   |
                |                                   |-------- ( P )
                |                                   |           |--------  text 
                |                                   |
                |                                   |-------- ( P )
                |                                   |           |--------  text 
                |------- ( SCRIPT )

</code></pre>

This framework ("tree") is then combined with the style information to create the layout, and serves as the interface for JavaScript to hook into.

##Browser Rendering         <a name="browser-rendering"></a>

![browser rendering](https://developer.mozilla.org/@api/deki/files/236/=Gecko_Overview_9.png)

That is Mozilla's render diagram. Most browsers are similar. In general, we can condense this to four processes:

- parse
- construct
- reflow (layout)
- paint



# Servers                                       <a name="servers"></a>
In most everyday scenarios, these are provided by a third party. They receive requests from clients, process the request, and respond with data, in the form of HTML & other files. There are (for the purposes of this tutorial), two levels of software: the server software itself (or “http daemon”), and the server-side languages (application software). Of these, PHP is by far the most prevalent, with more than 80% of websites using it. Second is ASP.NET, which is Microsoft’s proprietary software, and therefore evil, with almost 20%, and then Java, with 3%. Adobe has its own proprietary format, Coldfusion (1%). After that come the "higher-level" languages, in order: Perl, Ruby (primarily Ruby on Rails), Python, Javascript and then Lasso. &nbsp;(source: [w3techs][w3techs] )

## Dedicated Servers and Virtual Private Servers (VPS)  <a name="dedicated-servers"></a>
A dedicated server is what it sounds like. It's a server that's dedicated to one purpose (running your applications). It is a physical box, located somewhere in the world, who's sole purpose is to respond to requests made by your users, perform processing on those request, and then serve applications and data. There was a time when this was the only type of server. Now we have virtualisation technology, allowing hosting companies to set up large server farms, containing many boxes linked together to share processing and data storage. A virtual private server is a virtual machine (VM) that provides a 'virtual' operating system (OS) running within the immense field of networked power maintained by these farms. In a similar way that the Parallels or VirtualBox software allow you to run different operating systems on your computer, within the main OS, and while it is still running. A VPS is _distributed_ physically (and possibly geographically), and will be allocated system resources as needed, resulting in greater efficiency under low loads, while still allowing for high load situations without crashing the server.

## Shared Hosting <a name="shared-hosting"></a>
The budget option that most providers offer is shared hosting. In this configuration, a single machine (virtual or physical) will host multiple sites and/or applications, according to the address through which it is accessed. With this hosting package the site admin has limited access to the physical machine, and typically may only access the public html folder. This allows the admin to create, edit and delete the content served by the machine, but little or no access to server software itself. (Which is good, from a security standpoint.)

### A Quick Note about Apache       <a name="apache"></a>
The Apache HTTP Server, commonly referred to as Apache, is a web software program that has played a key role in the initial growth of the World Wide Web. In 2009 it became the first web server software to pass the 100 million website milestone. It’s estimated to serve 63.7% of all active websites and 58.49% of the top servers across all domains (December 2012). It’s what GoDaddy uses by default. It is very customisable, with modules for authentication, secure sockets layer and transport layer security, url redirection, data-compression “on-the-fly”, and support for all common programming languages. However, many languages provide their own servers.

### There are, of course, many other HTTP servers... <a name="Other-HTTP-Servers"></a>

## Content Distribution Networks (CDNs) <a name="CDNs"></a>
Many modern applications and sites operate a Content Distribution Network (CDN). Using this model, the server is mirrored across many locations, and the DNS routes the HTTP request to the closest (or otherwise most available) server to the user.