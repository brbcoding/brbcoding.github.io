---
layout: post
title: "Creating loading spinners with pure CSS"
date: 2013-12-05 17:54:14 -0500
comments: true
categories: [CSS animation, Sass, Scss, spinners]
---

<h3>The HTML</h3>
<hr />
<br />
HTML is pretty minimal in this example... We can create the simplest of loading spinners with just one single DOM element. Here's how it looks:  

``` html spinner.html
<div class="spinner"></div>
```

That's all the HTML we need to create our spinner.



<h3>The CSS</h3>
<hr />
<br />
<h3>Creating the Shape</h3>
<br />
``` css spinner.css
.spinner {
	width:  5em;  
	height: 5em;
	border-top:    0.75em solid red;
	border-left:   0.75em solid green;
	border-right:  0.75em solid blue;
	border-bottom: 0.75em solid orange;
	border-radius: 50%;
}
```  

The width and the height are up to you. To make a circle, they need to be the same (obviously). I'll be using borders to create a "donut" shape. The border width can vary, but between 0.5 and 1 em seemed to look good here. Then, we round the (currently square) div by giving it a `border-radius` of 50%.

<h3>Animating the Shape</h3>
<br />
**Disclaimer:** Your mileage may vary on the vendor prefixes. I generally use compass w/ Sass or [Lea Verou's Prefix Free](http://lea.verou.me/prefixfree/), so most of these prefixes were looked up and not totally tested across all browsers. 

```
.spinner {
	/* previous shape omitted */
	-webkit-animation: spin 2s infinite linear;
	-moz-animation:    spin 2s infinite linear;
	-o-animation:      spin 2s infinite linear;
	animation:         spin 2s infinite linear;
}

@-webkit-keyframes spin {
	100% { -webkit-transform: rotate(360deg);}
}

@-moz-keyframes spin {
	100% { -moz-transform: rotate(360deg); }
}

@-o-keyframes spin {
	100% { -o-transform: rotate(360deg); } 
}
@keyframes spin {
	100% { transform: rotate(360deg);   }
}
```

The spinning animation is actually very simple. Using `keyframes`, we can simply transform our shape 360 degrees in the amount of time specified in the `animation`. You can play with the different easing functions (`linear, ease, cubic-bezier(), ...`) and choose which animation you like best. 

<h3>The Demo</h3>
<h4>(May need a refresh to see spinning)</h4>
<p data-height="268" data-theme-id="2905" data-slug-hash="Jpums" data-user="brbcoding" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/brbcoding/pen/Jpums'>Jpums</a> by Cody Henshaw (<a href='http://codepen.io/brbcoding'>@brbcoding</a>) on <a href='http://codepen.io'>CodePen</a></p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

<h3>Just for fun... No extra html, just the body element and pseudo-elements</h3>
<h4>(May need a refresh to see spinning)</h4>
Keep in mind, this isn't very practical. You *could* add a class to the body and work off of that and make it slightly better, but you're probably better off just creating an element and hiding it until you need it.  
This demo uses prefix free as well as Sass (Scss syntax).  
``` scss spinner.scss ```
$gray: rgba(0, 0, 0, 0.75);
body {
	&:after {
	content: "";
	width: 5em;
	height: 5em;
	position: absolute;
	top: 0; bottom: 0; right: 0; left: 0;
	margin: auto;
	border-top: 0.5rem solid $gray;
	border-right: 0.25rem solid transparent;
	border-left: 0.5rem solid $gray;
	border-radius: 50%;
	animation: spin 1.5s infinite linear;
	}
}

@keyframes spin {
	 100% { transform: rotate(360deg); }
}
```

By using only 3 borders, we are able to create a different type of spinner. The `border-radius` again creates the rounded shape of the spinner. The `keyframes` just rotate the pseudo-element 360 degrees over the duration of the `animation`. With a `linear` easing function, we create a smooth spinning effect.  

<p data-height="252" data-theme-id="2905" data-slug-hash="axyDz" data-user="brbcoding" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/brbcoding/pen/axyDz'>axyDz</a> by Cody Henshaw (<a href='http://codepen.io/brbcoding'>@brbcoding</a>) on <a href='http://codepen.io'>CodePen</a></p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

Now you should have an awesome spinner... Play around with different animations, directions, colors, etc... to make it your own. You can also use pseudo-elements to create multiple spinner shapes, positioned absolutely on top of one another. This can create a cool effect as well. That's beyond the scope of this post, but here's you can see this in action [here](http://codepen.io/brbcoding/full/pLxgF). Thanks for stopping by and feel free to say hi @CodyHenshaw.