---
layout: post
title:  "Fun with Custom CSS in Kanbanery"
date:   2015-04-30 12:21:00
comments: true
categories: Design
---

I'm learning CSS and what better playground (other than this blog) than my product, [Kanbanery.com](http://kanbanery.com).

One of the features of the Pro plan at Kanbanery is that ability to apply custom CSS. Some people use it to make the header match their logo colors, but I wanted to try to completely change the look and feel of the site. 

Here's a step-by-step tutorial about how I made an innocent Kanbanery board, known for it's professional and elegant style, into this monstrosity:

![After Custom CSS]({{ pklipp.github.io }}/assets/12.png)

I created a board with some tasks and users to use as my CSS playground. Here's what it looked like before adding any custom CSS. I did upload a custom logo and created user accounts with superhero logos as Gravatars.

![Before Custom CSS]({{ pklipp.github.io }}/assets/13.png)

Next, I created a blank CSS file and hosted it on my own web server so I could make updates quickly and see the results live. I pasted the URL into the form on the Custom CSS tab in my Kanbanery board.

Then, I had to decide which elements to change, and what they were called. The easiest way I found to do that was to use the inspector in Chrome Developer Tools and click on the elements that I wanted to change.

One by one, I selected elements and changed their background colors to fit the superhero theme. 

{% highlight css %}  
/* match the header color to the logo background */
#header {
  background-color: RGB(40, 115, 190) !important;
}

/* Make the tabs black */
a.toggle {
  background-color: black !important;
}
{% endhighlight %}

I noticed that my changes didn't work consistently and faced a common frustration that I have with CSS and that's the C part. The fact that the style sheets are cascading is super powerful, but keeping track of those inheritances when you're just starting out and haven't developed a good style for managing large CSS files or collections of files is tricky. It's doubly so when intentionally overriding styles, but a friend told me an easy work around. Just add the tag !important, and no matter in what order the styles are loaded, the one from the external stylesheet that is intended to override existing styles will be applied.

Then, to make it really wacky, I replaced the solid grey background of the board with a repeating image:

{% highlight css %}
/* Change the background of the board */
#content {
	background-image: URL(http://paulklipp.com/images/pow.jpg) !important;
}
{% endhighlight %}

Suddenly, I couldn't read the deadline warnings, so I set their background color to white:

{% highlight css %}
/* set deadline background color */
.task-deadline {
	background-color: white !important;
}
{% endhighlight %}

I've never much liked the row at the top of the board which serves only to expand and collapse columns. It's a bit redundant if you don't have a lot of columns, so I removed it by setting its height to zero:

{% highlight css %}
/* Hide the bar with the column names */
.board-top-bar {
  height: 0px !important;
}
{% endhighlight %}

Several people have asked about changing the column width so they can fit more columns on the screen. The width that our designer set is, I think, the most attractive, but I found a narrower width that works fine:

{% highlight css %}
/* Make the columns more narrow */
li.column-view {
  width: 200px !important;
}

/* Make the task card more narrow */
.task-card {
	width: 200px !important;
	background-color: yellow !important;
}
{% endhighlight %}

The board now looked much too fun for the default font. Initially I set the font to Comic Sans, but working with browser fonts is really limiting so I learned to use custom fonts, also hosted on my private server:

{% highlight css %}
/* Set default font */
@font-face {
    font-family: 'comic';
    src: url('http://paulklipp.com/images/comic.ttf');
}

/* Change the font */
body {
  font-family: "comic", cursive !important;
}
{% endhighlight %}

And then, just to learn how to work with shadows, I added a drop shadow around the the avatars like this:

{% highlight css %}
/* Add a drop shadow around user avatar */
.task-owner {
	-webkit-box-shadow: 2px 2px 15px 1px rgba(0,0,0,0.75) !important;
-moz-box-shadow: 2px 2px 15px 1px rgba(0,0,0,0.75) !important;
box-shadow: 2px 2px 15px 1px rgba(0,0,0,0.75) !important;
}
li.column-view {
	width: 250px !important;
}
{% endhighlight %}

I'm not a fan of drop shadows, but I wanted to know how to do them with CSS because I haven't touched CSS since before CSS3, so I left them in.

And the final result, which will probably infuriate the original designer, demonstrates just how much control the custom stylesheets feature gives to Kanbanery users. If you've customized your Kanbanery board with custom stylesheets, I'd love to see a screenshot.




