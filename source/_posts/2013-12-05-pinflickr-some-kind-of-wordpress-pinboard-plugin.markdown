---
layout: post
title: "pinflickr - some kind of wordpress pinboard plugin"
date: 2013-08-05 14:09:27 -0500
comments: true
categories: [wordpress, php, flickr]
---

<p>I have just completed the first version of my &ldquo;Pinflickr&rdquo; plugin which automatically generates a pinboard styled gallery. Below is a paste of the Readme file located in the git repo. Full write-up coming soon.</p>

<p><a href="https://github.com/brbcoding/pinflickr/tree/master/wp-pinflickr">Full Source on Github</a></p>

<p>This plugin uses the Flickr API to build a pinboard style gallery on an existing Wordpress site.</p>

<p>Examples:</p>

<p><img src="http://i.imgur.com/DxAHfvp.jpg" alt="Screenshot 1" />
<img src="http://i.imgur.com/vzB3ljs.jpg" alt="Screenshot 2" /></p>

<h1>Installation</h1>

<ul>
<li>Move wp-pinflickr folder to the <code>plugins</code> directory of your Wordpress site.</li>
<li>Create a new API code and app secret on flickr <a href="http://www.flickr.com/services/developer/api/">More Info</a></li>
<li>Access <em>Pinflickr Settings</em> under the <em>Settings</em> menu inside the Wordpress Admin Menu.</li>
<li>Enter your API code and App Secret from Flickr. Save these changes.</li>
<li>Create a new page that will hold your gallery</li>
<li>The plugin works with a shortcode to display the gallery. The format is as follows:</li>
</ul>


<p><code>[pinflickr user_id="66956608@N06" tags="tags,separated,by,commas"]</code></p>

<p>The easiest way to find a user id is by using the site <a href="http://idgettr.com/">idGettr</a>.</p>

<ul>
<li>Enter the shortcode with your <code>user_id</code> and desired <code>tags</code> and save this page.</li>
<li>That&rsquo;s it! You&rsquo;ve created an awesome pinboard styled gallery!</li>
</ul>


<p><em>Working Demo Coming Soon</em></p>
