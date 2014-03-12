---
layout: post
title: "Server Side Languages"
modified: 2014-03-05 18:32:39 -0700
tags: [Server Side Languages, Languages, Servers]
image:
  feature: 
  credit: 
  creditlink: 
comments: true
share: true
series: "The Modern Web"
---

What we have seen up to now is enough. It is sufficient to serve a full working web page, and it is how the world wide web worked for many years (without the CSS and Javascript parts, even). However, HTML is a static markup language, and it doesn't serve well to allow the delivery of dynamically updating data and documents. For this we need something more complex, and there are a wealth of options available to us...

Market share statistics from [w3techs][w3techs].

## PHP: ( 80.1% of market share &uarr; )            <a name="php"></a>
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

## ASP.NET: ( 19.8% &darr;)             <a name="asp"></a>
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

## Java: ( 3.0% &darr; )                <a name="java"></a>
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

## ColdFusion: ( 0.9% &darr; )              <a name="coldfusion"></a>
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

## Perl: ( 0.7% &darr; )            <a name="perl"></a>
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


## Ruby: ( 0.4% &darr; )            <a name="ruby"></a>
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

## Python: ( 0.2% &darr; )          <a name="python"></a>
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
~~~

## JavaScript (Node.js) : ( 0.04% &uarr; )          <a name="server-side-js"></a>
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

[w3techs]: http://w3techs.com/technologies/overview/programming_language/all