---
layout: post
title: "CSS Variables in Firefox - AKA Variable Verbosity"
date: 2013-12-16 09:04:09 -0500
comments: true
categories: [CSS, HTML, Variables]
---

So, I saw this tweet from [Chris Heilmann](https://twitter.com/codepo8).  

<blockquote class="twitter-tweet" lang="en"><p>CSS Variables in Firefox Nightly 29: <a href="http://t.co/sEFrYiURjq">http://t.co/sEFrYiURjq</a> via <a href="https://twitter.com/YouTube">@YouTube</a></p>&mdash; Christian Heilmann (@codepo8) <a href="https://twitter.com/codepo8/statuses/411692052993159168">December 14, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>  

Awesome... maybe. I grabbed a fresh copy of FF Nightly and got to playing. The [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables) give a couple of examples... Here's another.  

<iframe width="100%" height="300" src="http://jsfiddle.net/pfyqn/embedded/css,result" allowfullscreen="allowfullscreen" frameborder="0"></iframe>  

So, in this example, we don't use any variables at all. We do, however, repeat the color `#bada55` **FOUR** times. I'm primarily a backend developer, and this redundancy kind of gives me the chills... Thanks to CSS Variables, however, we can eliminate some of this repetition. Here's another example, this time using variables... (Keep in mind, this will only work in Firefox 29 Nightly at the moment.)  

<iframe width="100%" height="300" src="http://jsfiddle.net/pfyqn/2/embedded/css,result" allowfullscreen="allowfullscreen" frameborder="0"></iframe>  

Pretty cool, right? It's not exactly *shorter*, but it is nice not having to remember hex values or color names...  

The title of this post included something along the lines of "Variable Verbosity", and that's not to discount the addition of variable support into browsers. I think it's awesome that the web is moving forward, just don't go throwing away your Sass or Less install just yet (obviously these tools do WAY more than just add variables). Here's how variables look when you use preprocessors vs. firefox's implementation (merely to show differences in implementation).  

<h4>Sass</h4>
``` css
$foo: #000000;
.bar {
	background: $foo;
}
```
<h4>Less</h4>
``` css
@foo: #000000;
.bar {
	background: @foo;
}
```
<h4>FF 29</h4>
``` css
/* invalid if not scoped */
:root {
	var-foo: #000000;
}
.bar {
	background: var(foo);
}
```  

Well, that about does it for this article. As you can see, the native implementation is much longer than the preprocessing variants, but hey, at least we're moving forward. I'll mess around with it a bit more, and see if I can come up with some cool stuff that shows that these are actually useful (beyond the evident use). If I've got any errors (which is not unlikely), please shoot me a note [@CodyHenshaw](https://twitter.com/CodyHenshaw) on twitter. Thanks for stopping by!

<h4>December 17, 2013 - Update: </h4>
So, after publishing this, something was brought to my attention. I had totally disregarded the concept of scope in this post, which is definitely one of the things that Mozilla did right with their variables. Scoped variables are helpful because they allow you to "silo" variables for use in specific parts of an application, or even declare them globally to be used throughout an application (in this case, a stylesheet). So, without further ado, let's get to scope.  

Scoping variables is trivial in both the Mozilla implementation, and with CSS preprocessors, like Sass. Here's what it looks like with CSS (again, only works in FF 29 at the time of writing).  

<iframe width="100%" height="300" src="http://jsfiddle.net/CHxsK/embedded/css,result" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

Here's how you do it with Sass... (You could also define a mixin with vars, and use them wherever you need to)  
<iframe width="100%" height="300" src="http://jsfiddle.net/n7frz/1/embedded/css,result" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

Either method works. Just wanted to throw this out there to show the scope capabilities of both native CSS and Sass. If someone wants to give me a Less example, I'd be happy to put it out there too. Thanks.

