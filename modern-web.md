---
layout: page
permalink: /modern-web/
title: The Modern Web
description: "A (not-very) brief introduction to the world you are living in."
tags: [Internet, web, technology]
image:
  feature: abstract-11.jpg
share: true
comments: true
---

# The Modern Web

# Clients, Servers, and other web hardware 	<a name="web-hardware"></a>

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

### The DOM (Document Object Model) 			<a name="dom"></a>
As a browser parses an HTML or xHTML document it creates the Document Object Model, which looks something like this:

<pre><code>
		|
		|--- ( HEAD )
		|		|
		|		|------- ( TITLE )
		|		|	
		|		|------- ( STYLESHEET )
		|		|	
		|		|------- ( SCRIPT )
		|		|
		|		|------- ( SCRIPT )
		|
		|--- ( BODY )
				|
				|------- ( DIV."container" )
				|				|
				|				|------------- ( DIV."header")
				|				|					|
				|				|					|---------- ( UL."navigation" )
				|				|								   |
				|				|								   |-------- ( A )
				|				|								   |		   |--------  text 
				|				|								   |
				|				|								   |-------- ( A )
				|				|								   			   |--------  text 
				|				|------------- ( DIV."main")
				|									|
				|								    |-------- ( P )
				|						  		    |		    |--------  text 
				|									|
				|									|-------- ( P )
				|									|			|--------  text 
				|------- ( SCRIPT )

</code></pre>

This framework ("tree") is then combined with the style information to create the layout, and serves as the interface for JavaScript to hook into.

##Browser Rendering 		<a name="browser-rendering"></a>

![browser rendering](https://developer.mozilla.org/@api/deki/files/236/=Gecko_Overview_9.png)

That is Mozilla's render diagram. Most browsers are similar. In general, we can condense this to four processes:

- parse
- construct
- reflow (layout)
- paint



# Servers										<a name="servers"></a>
Are (in our case) provided by GoDaddy. They receive requests from clients, process the request, and respond with data, in the form of HTML & other files. There are (for the purposes of this tutorial), two levels of software: the server software itself (or “http daemon”), and the server-side languages (application software). Of these, PHP is by far the most prevalent, with more than 80% of websites using it. Second is ASP.NET, which is Microsoft’s proprietary software, and therefore evil, with almost 20%, and then Java, with 3%. Adobe has its own proprietary format, Coldfusion (1%). After that come the "higher-level" languages, in order: Perl, Ruby (primarily Ruby on Rails), Python, Javascript and then Lasso. &nbsp;(source: [w3techs][w3techs] )

## Dedicated Servers and Virtual Private Servers (VPS) 	<a name="dedicated-servers"></a>
A dedicated server is what it sounds like. It's a server that's dedicated to one purpose (running your applications). It is a physical box, located somewhere in the world, who's sole purpose is to respond to requests made by your users, perform processing on those request, and then serve applications and data. There was a time when this was the only type of server. Now we have virtualisation technology, allowing hosting companies to set up large server farms, containing many boxes linked together to share processing and data storage. A virtual private server is a virtual machine (VM) that provides a 'virtual' operating system (OS) running within the immense field of networked power maintained by these farms. In a similar way that the Parallels or VirtualBox software allow you to run different operating systems on your computer, within the main OS, and while it is still running. A VPS is _distributed_ physically (and possibly geographically), and will be allocated system resources as needed, resulting in greater efficiency under low loads, while still allowing for high load situations without crashing the server.

## Shared Hosting <a name="shared-hosting"></a>
The budget option that most providers offer is shared hosting. In this configuration, a single machine (virtual or physical) will host multiple sites and/or applications, according to the address through which it is accessed. With this hosting package the site admin has limited access to the physical machine, and typically may only access the public html folder. This allows the admin to create, edit and delete the content served by the machine, but little or no access to server software itself. (Which is good, from a security standpoint.)

### A Quick Note about Apache 		<a name="apache"></a>
The Apache HTTP Server, commonly referred to as Apache, is a web software program that has played a key role in the initial growth of the World Wide Web. In 2009 it became the first web server software to pass the 100 million website milestone. It’s estimated to serve 63.7% of all active websites and 58.49% of the top servers across all domains (December 2012). It’s what GoDaddy uses by default. It is very customisable, with modules for authentication, secure sockets layer and transport layer security, url redirection, data-compression “on-the-fly”, and support for all common programming languages. However, many languages provide their own servers.

### There are, of course, many other HTTP servers... <a name="Other-HTTP-Servers"></a>

## Content Distribution Networks (CDNs) <a name="CDNs"></a>
Many modern applications and sites operate a Content Distribution Network (CDN). Using this model, the server is mirrored across many locations, and the DNS routes the HTTP request to the closest (or otherwise most available) server to the user.

# PHP and the Server Side Languages 	<a name="server-side-languages"></a>
What we have seen up to now is enough. It is sufficient to serve a full working web page, and it is how the world wide web worked for many years (without the CSS and Javascript parts, even). However, HTML is a static markup language, and it doesn't serve well to allow the delivery of dynamically updating data and documents. For this we need something more complex, and there are a wealth of options available to us...

Market share statistics from [w3techs][w3techs].

## PHP: ( 80.1% of market share &uarr; )			<a name="php"></a>
Since 1995. Originally the brain-child of one person, Rasmus Lerdorf, as a collection of scripts for his Personal Home Page, now developed by The PHP Group, and stands for PHP: Hypertext Preprocessor, currently version 5.3. Strongly tied to HTML, it can be embedded into HTML documents inline, as well as being used in autonomous scripts. It does not always produce HTML pages, and is really powerful enough to do lots of operating system level tasks on the server side. However, due to its history and nature, it is not always the most elegant solution for modern applications, but it does have a huge library of useful functions for processing common tasks. Lots of validation built in, as well as functions such as the mail() function, and database interactions. Wordpress and Joomla (and most sites) are built on PHP (interacting with a (SQL) database).

~~~ php
		<?php get_header(); ?>
			<?php if ( is_search() ) { ?>
				<div><h1>Congratulations!</h2><p>This is the search page</p></div>
			<?php } else { ?>
		<div id="splash">
			<div class="overlay gradient">
				<span class="sheila">Welcome</span>
				<span class="caption">TO YOUR<BR>GOOD &AMP; HEALTHY<BR>SOUTH DAKOTA<BR>INFORMATION<BR>CENTER.</span>

			</div>
			<ul id="sliderArray" style="display:none">
		<?php 
			$URI = '.' . substr( get_bloginfo( 'template_url' ) . '/images/HomeSlider*.*', 20 );
			foreach(glob( $URI ) as $filename){ 
				echo "<li> $filename </li>"; }	
		?>
			</ul> 
		</div>
		<script type="text/javascript" src=" <?php bloginfo( 'template_url' ) ?>/js/slider.js"></script></code></pre>
		<?php } ?>
~~~

## ASP.NET: ( 19.8% &darr;)				<a name="asp"></a>
Since 2002. A part of Microsoft’s .NET framework.  Programmed in a selection of languages. A really extensive platform, BUT... it’s Microsoft ;-(P



~~~ asp
		<%@ Page Language="C#" %>
		<!DOCTYPE html PUBLIC "---//W3C//DTD XHTML 1.0  //EN"
		"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
		<script runat="server">
		  protected void Page_Load(object sender, EventArgs e)  
		  {
		    // Assign the datetime to label control
		    lbl1.Text = DateTime.Now.ToLongTimeString();
		    lbl.Text = Ahmad();
		    lbl1.Text = DateTime.Now.ToShortTimeString();    
		  }
		</script>
		 
		<html xmlns="http://www.w3.org/1999/xhtml">
		<head runat="server">
		  <title>Sample page</title>
		</head>
		<body>
		  <form id="form1" runat="server">
		 
		 
		      The current time is: <asp:Label runat="server" id="lbl1" />
		 
		  </form>
		</body>
		</html>
~~~ 

## Java: ( 3.0% &darr; )				<a name="java"></a>
appeared in 1995, the brain child of James Gosling at Sun Microsystems (now Oracle Corporation), as a core component of the larger Java Platform. The Java platform is huge, not just for server applications, but also embedded Java “applets” in web pages (which offer secure functions through the platform), desktop software and entire computing platforms on embedded devices, mobile phones and enterprise servers and supercomputers. It has a syntax modelled on the lower-level languages C and C++, but is an Object-Oriented language. Java is (was) the standard development platform for many large enterprise systems. It is huge. However, the syntax is unwieldy, the processing is (relatively) slow, and although it’s not going anywhere any time soon, there are better languages for new development.


~~~ java
		// This is an example of a single line comment using two slashes
		 
		/* This is an example of a multiple line comment using the slash and asterisk.
		 This type of comment can be used to hold a lot of information or deactivate
		 code, but it is very important to remember to close the comment. */
		 
		/**
		 * This is an example of a Javadoc comment; Javadoc can compile documentation
		 * from this text.
		 */
		 
		/** Finally, an example of a method written in Java, wrapped in a class. */
		package fibsandlies;
		import java.util.HashMap;
		 
		public class FibCalculator extends Fibonacci implements Calculator {
		    private static HashMap<Integer, Integer> memoized = new HashMap<Integer, Integer>();
		 
		    /** Given a non-negative number FIBINDEX, returns,
		     *  the Nth Fibonacci number, where N equals FIBINDEX.
		     *  @param fibIndex The index of the Fibonacci number
		     *  @return The Fibonacci number itself
		     */
		    @Override
		    public static int fibonacci(int fibIndex) {
		        if (memoized.contains(fibIndex)) {
		            return memoized.get(fibIndex);
		        } else {
		            int answer = fibonacci(fibIndex - 1) + fibonacci(fibIndex - 2);
		            memoized.put(fibIndex, answer);
		            return answer;
		        }
		    }
		}
~~~ 

## ColdFusion: ( 0.9% &darr; )				<a name="coldfusion"></a>
ColdFusion is Adobe's web development platform. The language and platform were intially released in 1995, and wasn't purchased by Adobe until 2005. Originally designed to make it easier to connect simple HTML pages to a database, it quickly became a full platform  including an IDE and a "full" scripting language (that syntactically resembles Javascript) and now includes "advanced features" for enterprise integration and development of rich Internet applications.


~~~ cfml
		// CFML (ColdFusion Markup Language) has two alternative syntaxes

		/* This is the Tag syntax */

		<cfset ages = {jack = 11, brian = 12, tracy = 11} />
		<cfset ages.joey = 12 /> 
		<cfset ages["jill"] = 14 />

		<cfdump var = "#ages#" />

		<cfoutput>
			Joey is #ages["joey"]# years old.
		</cfoutput>

		/* This is the script syntax */

		<cfscript>
			ages = {jack = 11, brian = 12, tracy = 11};
			ages.joey = 12;
			ages["jill"] = 14;

			writeDump (var = ages);
			writeOutput ("Joey is #ages["joey"]# years old.");
		</cfscript>
~~~

## Perl: ( 0.7% &darr; )			<a name="perl"></a>
First developed in 1987 by Larry Wall, as a general purpose Unix scripting language. (We are now on Perl 5, with Perl 6 under development). It is somewhat of a swiss-army-knife language, very flexible and powerful. Perl 5 gained widespread popularity in the late ‘90s as a “CGI” (Common Gateway Interface) scripting language, in particular due to its parsing capabilities. (Parsing involves extracting meaningful data from an input “stream”). In 1998 it was referred to as the “duct tape that holds the internet together”, as it started to expand the capabilities of the web.


~~~ html
		#!/usr/bin/perl
		use strict;
		use warnings;

		use Path::Class;
		use autodie; # die if problem reading or writing a file

		my $dir = dir("/tmp"); # /tmp

		my $file = $dir->file("file.txt"); # /tmp/file.txt

		# Get a file_handle (IO::File object) you can write to
		my $file_handle = $file->openw();

		my @list = ('a', 'list', 'of', 'lines');

		foreach my $line ( @list ) {
		    # Add the line to the file
		    $file_handle->print($line . "\n");
		}
~~~ 


## Ruby: ( 0.4% &darr; )			<a name="ruby"></a>
Designed and developed by Yukihiro Matsumoto in the mid-90’s, Ruby is an object-oriented, multi-paradigm language. It is used to program full applications, in a similar way to Java (but nicer and better). Ruby is a language with a humorous personality. (Ruby on Rails less so). A large usage for the web is in the Ruby on Rails framework, which automates a lot of common coding patterns in building applications for the world wide web, including database access, layout templating, automated testing and more. Ruby on Rails is very popular in web application development at the present.

~~~ ruby
		get '/say/*/to/*' do
		  # matches /say/hello/to/world
		  params[:splat] # => ["hello", "world"]
		end

		get '/download/*.*' do
		  # matches /download/path/to/file.xml
		  params[:splat] # => ["path/to/file", "xml"]
		end
		---
		puts "What's your lucky number?"
		number = gets.chomp
		puts number.to_i
		output_number = number.to_i + 1
		puts output_number.to_s + ' is a bigger and better favorite number.'
~~~ 

## Python: ( 0.2% &darr; )			<a name="python"></a>
The brain-child of one Guido van Rossum, and the Python Software Foundation. It’s a general-purpose, high-level programming language, very powerful, with a design philosophy that emphasises code readability. It is used on the web in CGI scripts and full server implementations.



~~~ python
		import sys

		try:
		    f = open('myfile.txt')
		    s = f.readline()
		    i = int(s.strip())
		except IOError as e:
		    print "I/O error({0}): {1}".format(e.errno, e.strerror)
		except ValueError:
		    print "Could not convert data to an integer."
		except:
		    print "Unexpected error:", sys.exc_info()[0]
		    raise
~~~ html

## JavaScript (Node.js) : ( 0.04% &uarr; )			<a name="server-side-js"></a>
Not really related to Java, although the syntax was modelled on Java syntax. This is not a recent innovation in server-side technology, but is newly becoming popular. Javascript has been thought of merely as a scripting language, suitable for not more than interactive "gimmicks" on the web. However, it turns out that Javascript is actually a really powerful language (though not without its problems - primarily because it was written, from conception to public release, in a *ten*-day time span), that is superbly suited to server applications, because of its event-driven approach. 


~~~ javascript
		var http = require('http');
		 
		http.createServer(
		  function (request, response) {
		    response.writeHead(200, {'Content-Type': 'text/plain'});
		    response.end('Hello, world\n');
		  }
		).listen(8000);
		 
		console.log('Server running at http://localhost:8000/');
~~~ 



* * *

#Moving into the Present...
# HTML5, CSS3, and ES5/Strict	<a name="html5-css3-es5"></a>

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



# jQuery and other Javascript Frameworks and Libraries <a name="jquery"></a>

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

There are **looads** of different frameworks, and most of them are great. A lot of them do the same things. jQuery is a great one, providing a hugely solid base foundation for web programming.

# AJAX: Asynchronous JavaScript and XML <a name="ajax"></a>

AJAX is a dominant technology in current web development. Prior to AJAX, any state-changing interaction with the web page required a full page reload in the browser. And this was inefficient. In most cases, this results in a lot of the same data being re-sent to the browser on each user interaction. 

The innovation of AJAX is to allow the application to only load the data that is needed for the update of the application. When the user makes a change in the page that requires more data, a Javascript function is fired from behind-the-scenes, to ask the server for _just the information that is needed_. Previously, whenever the user clicked on a link on a page, the browser would reload an entire HTML page, with headers, all the page navigation, and then would need to cache-check all the images and other resources used on the page. All of this activity adds up, although we have become so used to it from using sites built with the previous paradigm.

This is the key to creating responsive web applications, that are able to keep a user's focus over a long series of interactions. At a neurological level, humans have a "distraction threshold" that is approximately 100 ms. That's a tenth of a second. We may not be conscious of this, and when trying to accomplish a task, we focus really hard and try to overcome this distraction, but on a physical level, we cannot respond in as focussed a manner when an application exceeds this distraction threshold. 

# Ruby on Rails, Python's Django, PHP's Zend or Laravel and others: Application Frameworks <a name="app-frameworks"></a>
Frameworks are built following common development practices. The developers have observed common activities and tasks that web developer's have been coding, over and over, and built a standard set of functions and methods to implement them. This allows more rapid development, as main core functions have been abstracted and standardised. There's no need to design and build standard procedures that have been used and re-uesd countless time over the last 20 years. These are already in place and available in short-hand methods.

Most frameworks are also highly *extensible*. Frameworks (especially) popular frameworks usually play well with other frameworks and libraries within their language, and incorporate many modules for all kinds of common- or not-so-common tasks. Chances are, if you are a humble developer, not breaking new ground, just trying to build useful applications, you will find that whatever you want to do has already been done. And most of the time, someone has made a plug-in or framework extension to make it easier. Ruby, Python, PHP, and many other open-source languages have a **HUGE** community of developers that use, play with, and help to build the language and it's extensions.

And frameworks make it incredibly easy to use a lot (or just a few) of these extensions. We call this working with a 'stack' of processing tools. For example, in my personal development work, I use SASS as a CSS pre-processor, and `git` for 'version' management. (I haven't got so far as to have discrete versions, but git is still a useful backup tool). Ruby on Rails implements both of these, and many other build tools such as grunt or require.js, to manage javascript file processing.

##SASS (Syntactically Awesome Style Sheets) <a name="sass"></a>
SASS is a CSS Pre-processor. Which means that it generates CSS. SASS extends standard CSS in a number of ways, but primary among them are the use of variables and functions. A variable allows us to define a value in a short-hand, that can be re-used throughout our code. For example:

	$titleRed = rgb(212,12,12);

This now allows us to use the `$titleRed` variable throughout our code, without having to remember the specific rgb values. It also allows us to change the value of $titleRed, and have all instances where we've used the variable update automatically.

SASS also allows us to abstract some of our mathematical calculations.

	#container {
		width: ($bodyWidth - 20) / 2;
	}

##HAML (HTML Abstraction Markup Language) <a name="haml"></a>
HAML provides a more concise and clear markup for writing HTML code, which can be interpreted by a higher-level language to render as standard HTML.

~~~ haml
	!!!
	%html{ :xmlns => "http://www.w3.org/1999/xhtml", :lang => "en", "xml:lang" => "en"}
	  %head
	    %title BoBlog
	    %meta{"http-equiv" => "Content-Type", :content => "text/html; charset=utf-8"}
	    %link{"rel" => "stylesheet", "href" => "main.css", "type" => "text/css"}
	  %body
	    #header
	      %h1 BoBlog
	      %h2 Bob's Blog
	    #content
	      - @entries.each do |entry|
	        .entry
	          %h3.title= entry.title
	          %p.date= entry.posted.strftime("%A, %B %d, %Y")
	          %p.body= entry.body
	    #footer
	      %p
	        All content copyright © Bob
~~~ 

HTML markup can be very wieldy and verbose, with each tag requiring an almost-identical closing tag. HAML abstracts this, and allows us to write HTML code in a format that is more readable (to developers, at least), more concise, and more akin to the format we use in the higher-level languages such as Ruby. It also allows us to embed Ruby processing code within the HTML code (in a more concise format than eRuby).

~~~ html
	<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
	<html lang='en' xml:lang='en' xmlns='http://www.w3.org/1999/xhtml'>
	  <head>
	    <title>BoBlog</title>
	    <meta content='text/html; charset=utf-8' http-equiv='Content-Type' />
	    <link href="/stylesheets/main.css" media="screen" rel="Stylesheet" type="text/css" />
	  </head>
	  <body>
	    <div id='header'>
	      <h1>BoBlog</h1>
	      <h2>Bob's Blog</h2>
	    </div>
	    <div id='content'>
	      <div class='entry'>
	        <h3 class='title'>Halloween</h3>
	        <p class='date'>Tuesday, October 31, 2006</p>
	        <p class='body'>
	          Happy Halloween, glorious readers! I'm going to a party this evening... I'm very excited.
	        </p>
	      </div>
	      <div class='entry'>
	        <h3 class='title'>New Rails Templating Engine</h3>
	        <p class='date'>Friday, August 11, 2006</p>
	        <p class='body'>
	          There's a very cool new Templating Engine out for Ruby on Rails. It's called Haml.
	        </p>
	      </div>
	    </div>
	    <div id='footer'>
	      <p>
	        All content copyright © Bob
	      </p>
	    </div>
	  </body>
	</html>
~~~ 

However, even more useful than HAML or SLIM, for web content producers, is a format known as...

##Markdown <a name="markdown"></a>

"Markdown is a text-to-HTML conversion tool for web writers. [It] allows you to write using an easy-to-read, easy-to-write plain text format, then convert it to structurally valid [HTML]."

It looks like this:

~~~ markdown
		Sample Markdown Cheat Sheet
		=========================== 

		This is a sample markdown file to help you write Markdown quickly :)

		If you use the fabulous [Sublime Text 2 editor][ST2] along with the [Markdown Preview plugin][MarkdownPreview], open your ST2 Palette with `CMD+P` then choose `Markdown Preview in browser` to see the result in your browser.

		## Text basics
		this is *italic* and this is **bold** .  another _italic_ and another __bold__

		this is `important` text. and percentage signs : % and `%`

		This is a paragraph with a footnote (builtin parser only). [^note-id] 

		Insert `[ toc ]` without spaces to generate a table of contents (builtin parser only).

		## Indentation
		> Here is some indented text
		>> even more indented

		## Titles
		# Big title (h1)
		## Middle title (h2)
		### Smaller title (h3)
		#### and so on (hX)
		##### and so on (hX)
		###### and so on (hX)

		## Example lists (1)

		 - bullets can be `-`, `+`, or `*`
		 - bullet list 1
		 - bullet list 2
		    - sub item 1
		    - sub item 2

		        with indented text inside

		 - bullet list 3
		 + bullet list 4
		 * bullet list 5

		## Links

		This is an [example inline link](http://lmgtfy.com/) and [another one with a title](http://lmgtfy.com/ "Hello, world").

		Links can also be reference based : [reference 1][ref1] or [reference 2 with title][ref2].

		References are usually placed at the bottom of the document

		## Images

		A sample image :

		![revolunet logo](http://www.revolunet.com/static/parisjs8/img/logo-revolunet-carre.jpg "revolunet logo")

		As links, images can also use references instead of inline links :

		![revolunet logo][revolunet-logo]


		## Code

		It's quite easy to show code in markdown files.

		Backticks can be used to `highlight` some words.

		Also, any indented block is considered a code block.  If `enable_highlight` is `true`, syntax highlighting will be included (for the builtin parser - the github parser does this automatically).

		    <script>
		        //document.location = 'http://lmgtfy.com/?q=markdown+cheat+sheet';
		    </script>

		## Math

		When `enable_mathjax` is `true`, inline math can be included \\(\frac{\pi}{2}\\) $\pi$

		Alternatively, math can be written on its own line:

		$$F(\omega) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{\infty} f(t) \, e^{ - i \omega t}dt$$

		\\[\int_0^1 f(t) \mathrm{d}t\\]

		\\[\sum_j \gamma_j^2/d_j\\]
~~~ 

[Official Markdown Syntax](http://daringfireball.net/projects/markdown/syntax)

[This document was written in Markdown.](http://clov3r.us/modern-web/condensed.md)

#Developer Tools <a name="developer-tools"></a>

##The IDE (Integrated Development Environment) <a name="ide"></a>
This is essentially a text-editor, but modern IDEs incorporate a host of features to make our lives easeier as developers, including syntax highlighting, auto-completion, and build scripts. My IDE of choice (Sublime Text) also incorporates incredibly useful feature integration with FTP and Git.

##Git (or or version-control software) <a name="git"></a>
Git tracks changes to files within our projects. It also provides powerful and convenient options to roll-back changes, or to merge changes from two or more sources, as git is built for *distributed* development. 

##FTP (File transfer protocol) <a name="ftp"></a>
Used to upload files to the remote host.

#Website Design Process <a name="design-process"></a>
It is important to remember that:
##Website Design is Product Design, not Graphic Design <a name="product-design"></a>
Print designers are used to designing for a 2-dimensional medium. Superficially, the web resembles this medium, as we primarily perceive it through the 2d screen, but it very quickly becomes apparent that the web is more than 3-dimensional (check [this](http://tympanus.net/Development/AnimatedBooks/index.html) out, for example). In addition to the virtual 3d, there are also the various data layers and [hyperlinking](http://www.w3.org/DesignIssues/) to take into account.

In addition, content on the web is much more fluid than its printed counterpart, and must be designed to fit on various types of screen. In print, we focus on pixel-perfect control, but with the wide variation in internet-accessible devices, and with the field only expanding, we have to relinquish this control and accept that it is ok if a webpage looks different when viewed across different platforms. 

### "Design is how it Works" <a name="how-it-works"></a>



## The Web is (and should be) 95% Typography <a name="typography"></a>

Despite platform inconsistencies, leading, word &amp; letter spacing, active white-space and dosed uses of color are key issues.

### Think of Text as a User Interface <a name="text-as-ui"></a>



## Work with Light, not layers of Color <a name="work-with-light"></a>



## Make fonts larger! <a name="make-fonts-larger"></a>

#### "A printed work which cannot be read becaomes a product without purpose"

The default font size on a browser is 16 pt (pixels), for a good reason. Most of us have good eyesight, but there are plenty of people using the web that don't.

## Paper wants Grey Noise, the Screen Doesn't <a name="paper-wants-grey-noise"></a>

Every extra word risks losing the reader

The goal is to stay simple... but without over-simplifying or being sensational, which works only for the "dumb" audience.



##Simplicity is Not a Given <a name="simplicity"></a>

###[iA.net](http://iA.net) <a name="ia_net"></a>



## Start with the Business Objectives <a name="business-objectives"></a>
It's a good idea to start the design process by looking at what the product is hoping to achieve. Without clearly defining the objectives of the website, it is easy to fall into the trap of producing web sites, 'just so that they're there'.

## Calls to Action <a name="calls-to-action"></a>
What is it that we want users to do once they reach our site? And what's the best way to help them achieve that goal?



# "Techne" (Greek) :-> "craft", "craftmanship", or "art" <a name="techne"></a>

[w3techs]: http://w3techs.com/technologies/overview/programming_language/all