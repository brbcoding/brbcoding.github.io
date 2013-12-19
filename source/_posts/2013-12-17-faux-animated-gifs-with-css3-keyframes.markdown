---
layout: post
title: "Faking an animated .gif with CSS keyframes"
date: 2013-12-17 16:31:31 -0500
comments: true
categories: [css3, keyframes, css animations]
---

Animated gifs can be pretty impactful if used correctly. They can illustrate a point without having to embed a video or a wall of text. The issue with gifs is that they are just pictures. They can't be stopped or started (though many people fake it by swapping a static image). I ran across a question on Stack Overflow which asked for a solution to stop (by stop, I mean freeze and don't reset) a gif on `:hover` and resume on mouseout. JavaScript plugins were immediately suggested, which might be the correct solution to this problem... but let's try it with CSS animations anyway.

The first thing we will need to do is break our .gif into frames. There are tons of tools online that allow you to do this, and I'd even guess that ImageMagick will do it for you as well. Here's the one I chose to start with:  

![bananananana](http://i.imgur.com/MxrP3DG.gif)

I broke mine into 8 individual frames. Here they are:  

![banana1](http://i.imgur.com/E2ee6fI.gif)
![banana2](http://i.imgur.com/JIi0uul.gif)
![banana3](http://i.imgur.com/owNGnNN.gif)
![banana4](http://i.imgur.com/2Ii6XOz.gif)
![banana5](http://i.imgur.com/ZmQBrQ5.gif)
![banana6](http://i.imgur.com/iAsfHyY.gif)
![banana7](http://i.imgur.com/AJwRblj.gif)
![banana8](http://i.imgur.com/fx5wUNY.gif)  

So, that's it for prep work... Let's get our html ready.

``` html
<div id="faux-gif"></div>
```

Yep, that's it... Now, let's add one of the images as a `background-image`.  
<div data-height="268" data-theme-id="2905" data-slug-hash="gqxEo" data-user="brbcoding" data-default-tab="css" class='codepen'><pre><code>#faux-gif { 
    position: absolute;
	top: 0; left: 0; right: 0; bottom: 0;
	margin: auto;
    
    background-image: url(http:&#x2F;&#x2F;i.imgur.com&#x2F;E2ee6fI.gif);
	background-repeat: no-repeat;
	background-attachment: fixed;
	background-position: center;
  
}</code></pre>
<p>See the Pen <a href='http://codepen.io/brbcoding/pen/gqxEo'>gqxEo</a> by Cody Henshaw (<a href='http://codepen.io/brbcoding'>@brbcoding</a>) on <a href='http://codepen.io'>CodePen</a></p>
</div><script async src="//codepen.io/assets/embed/ei.js"></script>

So, the cool part about this is that we are using `background-image`. The background image can be animated with keyframes. Therefore, we can use keyframes to change the url of the `background-image`! Just make sure to call the animation from within your `#faux-gif`... You can read more about keyframes on the [MDN Site](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes).  

A trivial example using just two images might be something like this. Note the `animation: giffy 0.5s infinite linear. That's how we make the animation actually run. 0.5s will be the duration of our animation called "giffy", it will run indefinitely, and it will have a linear timing function (as opposed to ease, ease-in-out, etc...):  

<div data-height="268" data-theme-id="2905" data-slug-hash="urHce" data-user="brbcoding" data-default-tab="css" class='codepen'><pre><code>#faux-gif {
	position: absolute;
	top: 0; left: 0; right: 0; bottom: 0;
	margin: auto;
	background-image: url(http:&#x2F;&#x2F;i.imgur.com&#x2F;E2ee6fI.gif);
	background-repeat: no-repeat;
	background-attachment: fixed;
	background-position: center;
	width: 300px;
	height: 300px;
	animation: giffy 0.5s infinite linear;
}


@keyframes giffy {
	from   { background-image: url(&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;E2ee6fI.gif&#x27;); } 
	to { background-image: url(&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;fx5wUNY.gif&#x27;); }
}</code></pre>
<p>See the Pen <a href='http://codepen.io/brbcoding/pen/urHce'>urHce</a> by Cody Henshaw (<a href='http://codepen.io/brbcoding'>@brbcoding</a>) on <a href='http://codepen.io'>CodePen</a></p>
</div><script async src="//codepen.io/assets/embed/ei.js"></script>



We have an almost-gif now... We just need to add the other frames. The cool part about keyframes is that you can use percentages instead of `to{ } ... from{ }`. Let's see how many we will need... We have 8 frames total, and 100% duration to work with. You may first think that you'll work in increments of 12.5%. That would be fine, but we haven't taken into account that our first frame is already taken care of with the initial state. That's the value we'll use at 0%. Instead, we'll want to do 100 / 7 (rounded to something simple to work with)... I'll just use 14.25%. Now, we'll create keyframes from 0% - ~100% in increments of 14.25%.  

<div data-height="268" data-theme-id="2905" data-slug-hash="Kiumf" data-user="brbcoding" data-default-tab="css" class='codepen'><pre><code>#faux-gif {
	position: absolute;
	top: 0; left: 0; right: 0; bottom: 0;
	margin: auto;
	background-image: url(http:&#x2F;&#x2F;i.imgur.com&#x2F;E2ee6fI.gif);
	background-repeat: no-repeat;
	background-attachment: fixed;
	background-position: center;
	width: 300px;
	height: 300px;
	animation: giffy 0.5s infinite linear;
}

#faux-gif:hover {
	animation-play-state:paused;
}

@keyframes giffy {
	0%   { background-image: url(&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;E2ee6fI.gif&#x27;); } 
	14.25%  { background-image: url(&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;JIi0uul.gif&#x27;); }
	28.5%  { background-image: url(&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;owNGnNN.gif&#x27;);}
	42.75%  { background-image: url(&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;2Ii6XOz.gif&#x27;); }
	57%  { background-image: url(&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;ZmQBrQ5.gif&#x27;); }
	71.25%  { background-image: url(&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;iAsfHyY.gif&#x27;); }
	85.5%  { background-image: url(&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;AJwRblj.gif&#x27;); }
	99.75% { background-image: url(&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;fx5wUNY.gif&#x27;); }
}</code></pre>
<p>See the Pen <a href='http://codepen.io/brbcoding/pen/Kiumf'>Kiumf</a> by Cody Henshaw (<a href='http://codepen.io/brbcoding'>@brbcoding</a>) on <a href='http://codepen.io'>CodePen</a></p>
</div><script async src="//codepen.io/assets/embed/ei.js"></script>

And that's about it. You can play with the animation timing, the duration, etc... You couldn't do that with your .gif, now could you? You'll see that I also added a `:hover` state. That was to satisfy the requirements of the Stack Overflow post I was solving with this technique. Thanks for checking it out, please let me know what mistakes I have made, and say hi [@CodyHenshaw](https://twitter.com/CodyHenshaw) on twitter. 

<h4>Update: December 9th</h4>
So, I was testing this method, and it seems that it doesn't work in firefox. I wrote this quick n' dirty FauxGif "class" to take care of that. This doesn't demonstrate pre-loading of the images, which is something you will want to do if you don't want to see blank frames.  

<div data-height="268" data-theme-id="2905" data-slug-hash="JhroI" data-user="brbcoding" data-default-tab="js" class='codepen'><pre><code>window.onload = function() {

	function FauxGif(element, frames, speed) {
		this.currentFrame = 0,
		this.domElement   = element,
		this.frames       = frames || null,
		this.speed        = speed  || 200;
		this.interval;
		this.init();
	}

	FauxGif.prototype = {
		init: function() {
			&#x2F;&#x2F; set the first one to the first image
			console.log(this.frames[0])
			this.domElement.style.backgroundImage = &quot;url(&quot; + this.frames[0] + &quot;)&quot;;
		},
		pause: function() {
			clearInterval(this.interval);
		},
		resume: function() {
			var that = this;

			that.interval = setInterval(function(){
				console.log(that.frames[that.currentFrame])
				console.log(that.frames.length);
				that.currentFrame &lt; that.frames.length - 1 ? that.currentFrame++ : that.currentFrame = 0;
				that.domElement.style.backgroundImage = &quot;url(&quot; + that.frames[that.currentFrame] + &quot;)&quot;;
			}, 200);
		}
	}

	var frames = [
					&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;E2ee6fI.gif&#x27;,
					&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;JIi0uul.gif&#x27;,
					&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;owNGnNN.gif&#x27;,
					&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;2Ii6XOz.gif&#x27;,
					&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;ZmQBrQ5.gif&#x27;,
					&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;iAsfHyY.gif&#x27;,
					&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;AJwRblj.gif&#x27;,
					&#x27;http:&#x2F;&#x2F;i.imgur.com&#x2F;fx5wUNY.gif&#x27;
				]

	var elem = document.querySelector(&#x27;#faux-gif&#x27;),
		gif  = new FauxGif(elem, frames);


	elem.addEventListener(&#x27;mouseenter&#x27;, function(){
		gif.resume()
	});

	elem.addEventListener(&#x27;mouseleave&#x27;, function() {
		gif.pause();
	});
}</code></pre>
<p>See the Pen <a href='http://codepen.io/brbcoding/pen/JhroI'>JhroI</a> by Cody Henshaw (<a href='http://codepen.io/brbcoding'>@brbcoding</a>) on <a href='http://codepen.io'>CodePen</a></p>
</div><script async src="//codepen.io/assets/embed/ei.js"></script>

Again, let me know if I have any issues. Thanks for stopping by.