---
layout: post
title: "Icon fonts and pseudo-elements: They were made for one another."
date: 2013-09-15 14:07:21 -0500
comments: true
categories: [css, html, pseudo-elements] 
---

<p>Using icon fonts with pseudo-elements is ridiculously easy. Choosing between icon font sets will take a lot longer than the actual implementation. I&rsquo;ll give an example below with some icons from the super popular <strong><a href="http://fortawesome.github.io/Font-Awesome/">font awesome</a></strong> set. We will import the icons from <strong><a href="http://twitter.com/TimPietrusky">@TimPietrusky&rsquo;s</a></strong> always useful, <strong><a href="http://weloveiconfonts.com/">weloveiconfonts</a></strong>.</p>

<pre class="codepen" data-height="300" data-type="css" data-href="KwHkf" data-user="brbcoding"><code> </code></pre>


<script async src="http://codepen.io:/assets/embed/ei.js"></script>


<h3>Locating the values to use for each icon</h3>

<p>I personally run Chrome in my day-to-day, so I generally use devtools for a lot of my testing&hellip; Here are some screenshots illustrating the &ldquo;look up&rdquo; process for these icon fonts. We will start by looking at the <strong><a href="http://fortawesome.github.io/Font-Awesome/icons/">Cheat Sheet</a></strong> on the font awesome github page.</p>

<p>First, select an icon font. You&rsquo;ll be taken to the corresponding page which displays that icon in different sizes. From here, there are two ways we can go about finding the actual unicode value.</p>

<ol>
<li>It will be displayed in light gray next to the icon font&rsquo;s title.
<img src="http://i.imgur.com/2OnWpUg.png" alt="Unicode 1" /></li>
<li>More commonly, you&rsquo;ll need to check out the source to find out the corresponding unicode. To do this, right click an icon font and click <code>inspect element</code>. You may have to scroll a bit to find it, but in the styles view on the right-hand side, you&rsquo;ll find a css declaration that looks very similar to the example we used before.<br/>
<img src="http://i.imgur.com/AHX5sRC.png" alt="Unicode 2" /></li>
</ol>


<p><em>That&rsquo;s it! We can put icon fonts <strong>everywhere</strong> now! (don&rsquo;t do that, seriously.)</em></p>
