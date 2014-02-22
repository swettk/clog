---
layout: post
title: "The Y-Combinator in ECMAScript 6: A Function of Beauty and Elegance"
modified: 2014-02-21 16:37:28 -0700
tags: [ECMAScript 6, Programming Languages]
image:
  feature: 
  credit: 
  creditlink: 
comments: true
share:    true
---

<!--This is the y-combinator in [Scheme](http://scheme.org):

{% highlight scheme %}
(define (Y f)
  ((lambda (x) (x x))
   (lambda (g)
     (f (lambda args (apply (g g) args))))))
 
(define fac
  (Y
    (lambda (f)
      (lambda (x)
        (if (< x 2)
          1
          (* x (f (- x 1))))))))
 
(fac 5) ; 120
{% endhighlight %}-->

This is the y-combinator in [ClojureScript/Clojure](http://link-here):

{% highlight clojure %}
(defn Y [le]
  ((fn [f] (f f))
   (fn [f] 
     (le (fn [args] ((f f) args))))))

(def factorial 
  (Y (fn [fac] 
       (fn [n] 
         (if (< n 2) 
           1
           (* n (fac (dec n))))))))
 
(factorial 5) ;; 120
{% endhighlight %}

This is the y-combinator function and factorial implementation in JavaScript/ES5:

It has been described as a [thing of beauty](http://weblog.bocoup.com/little-javascripter-revisited), 
but to my eye, there's as much boiler-plate as beauty:

{% highlight javascript %}
function Y(le) {
  return (function (f) {
    return f(f);
  }(function (f) {
    return le(function (x) {
      return f(f)(x);
    });
  }));
}

 
var factorial = Y(function (fac) {
  return function (n) {
    return n <= 2 ? n : n * fac(n - 1);
  };
});
 
factorial(5); // 120
{% endhighlight %}

Now here's the same function, but implemented using the new *harmony* syntax of ES6.

{% highlight javascript %}
let Y =
  (le => (f => f(f))
    (f => le((...args) => f(f)(...args))));
 
let factorial =
  Y(f => (n =>
    (n < 2 ?
      1 :
      n * f(n - 1))));
 
factorial(5); // 120
{% endhighlight %}

Now that's pretty.