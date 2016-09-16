---
layout: post
title:  "Exploration 1: D3.js"
date:   2016-09-14
categories: process
---

## Intro

If you ask a class to find search the web for cool data visualizations, there is a pretty big chance one of them will find something that uses [D3.js][d3]. D3 seems to be the go-to javascript library when it comes to data vis on the web. It was created by the ex-editor of the New York Times Graphics Department, Michael Bostock.

I have used D3 before, but was only able to make stuff happen by copying bits and pieces from examples and constantly struggling. I was never able to appreciate the power and efficiency that D3 is known for.

If anyone currently in YSDN has preached about the benefits of using code to work with data, it's me. I think coding with data is one of the best ways to work with it, it feels freeing and efficient. You don't want to spend ten hours tediously arranging lines in illustrator to find out that you don't like that type of visualization anymore. With code you have this incredible opportunity to _play_ with data.

Therefore, with this project I wanted to finally figure out the basics of D3, the initial mental model I had skipped over last time. With the recent release of D3 4.0, it seemed like a better time than ever.

Side Note: For a great read about the design of D3 4.0 and software in general, look here: _[What Makes Software Good?][d3-4]_

Now before you read the next part, go read the introduction on the [D3 Page.][d3] I'm going to go over the parts that I don't think are very clear in the intro.

## Explaining the Confusing Parts

I've heard that D3 has some of the best source code and documentation of almost any software, but it can be a lot to take in.

The most important thing I've read about using D3 so far is this: 

> Instead of telling D3 how to do something, tell D3 _what_ you want.

Data-Joins are one of the main ideas in D3, and are one of the reasons D3 is so powerful. The quote above really helped me wrap my head around the idea of Data-Joins in D3. From [this article.][data-joins]

Instead of having to loop through each data-entry in your data, you simple tell D3 what you want it to do for each data-entry.

### The Common Data Pattern
When working with data in D3 this is a common pattern you will go through. 

{% highlight javascript %}
var text = g
  .selectAll("text")
  .data(data, key); // JOIN

var js = "nope";

text.exit() // EXIT removes the "leftover" data
    .remove();

text.enter() // ENTER the new data
  .append("text")
    .text(function(d) { return d; })
  .merge(text) // MERGE new data with current data
    .attr("x", function(d, i) { return i * 32; });
{% endhighlight %}


### Enter and Exit Selections
Another fundamental idea in D3 is the idea of Enter and Exit selections, as seen above! These selections are fundamental to how you will work with data in D3. I'm going to quote these definitions directly: 

- The _enter()_ selection represents “missing” elements (incoming data) that you may need to create and add to the document.
- The _exit()_ selection represents “leftover” elements (outgoing data) that you may need to remove from the document.

As seen above, after you join the new data to your selection you are going to want to use the _exit()_ selection to get rid of the data that is no longer relevant. After that, you'll want to use _enter()_ to select the new data, then _merge()_ that into the current data. After that you'll have the data you want selected and you're free to do whatever you please with it!

Still confused? Don't worry, it took me a while.
To help those of you who need to get their hands dirty to understand, I have made an example of these concepts on Codepen, which you can find below. Open up the 'Babel' tab to see some well commented javascript waiting for you. I recommended opening it in Codepen so you can read the code easier and edit it for yourself to play around.

<p data-height="533" data-theme-id="light" data-slug-hash="zKvmzm" data-default-tab="result" data-user="huntercaron" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/huntercaron/pen/zKvmzm/">d3-play</a> by Hunter Caron (<a href="http://codepen.io/huntercaron">@huntercaron</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Happy Hacking!

[d3]: https://d3js.org/
[d3-4]: https://medium.com/@mbostock/what-makes-software-good-943557f8a488#.ow8b82goy
[data-joins]: https://bost.ocks.org/mike/join/
