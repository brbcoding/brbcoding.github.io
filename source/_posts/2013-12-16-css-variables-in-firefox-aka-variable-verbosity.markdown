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

<iframe width="100%" height="300" src="http://jsfiddle.net/pfyqn/embedded/result,css" allowfullscreen="allowfullscreen" frameborder="0"></iframe>  

So, in this example, we don't use any variables at all. We do, however, repeat the color `#bada55` **FOUR** times. I'm primarily a backend developer, and this redundancy kind of gives me the chills... Thanks to CSS Variables, however, we can eliminate some of this repetition. Here's another example, this time using variables... (Keep in mind, this will only work in Firefox 29 Nightly at the moment.)  

<iframe width="100%" height="300" src="http://jsfiddle.net/pfyqn/2/embedded/result,css" allowfullscreen="allowfullscreen" frameborder="0"></iframe>  

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


