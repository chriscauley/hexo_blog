title: "Smcameron's curly vortex"
date: 2014-04-19 14:35:44
tags:
- smcameron
- TXRX Labs
- programming
- processing
post_asset_folder: true
comments: false
---

I missed out on the [April Recreational Programming Group](http://txrxlabs.org/blog/smcameron/recreational-computer-programming-group-april-2014/) because I was at PyCon. He presented on a really cool texture genreator. It's written in Processing so I decided to see how easy it is to run it using [processing.js](http://processingjs.org/). TL;DR - Really easy.

The only necessary change I had to make to the code was to add a note to preload the image. Normally processing will execute assuming that the image file is local, but the DOM hasn't yet loaded the image. To do this you just add a comment to preload the image:

{% codeblock curly_vortex lang:java %}
/* @pjs preload="13940260644_7fe66ea59c_c.jpg" */;
String source_image_file = "13940260644_7fe66ea59c_c.jpg";
int xdim = 300;//1400;
int ydim = 300;//700;
int nparticles = 50000;
{% endcodeblock %}

I also resized it and changed the image. I wanted to add the ability to input an image url via a text field and so that any visitors can change the image. This, it turns out isn't possible. The preload string cannot use a javascript variable. Also since the image is loaded via ajax, cross site scripting considerations prevent it. I could do this using a django app that would dynamically rewrite the pde file, but I don't want to host a place for people to randomly upload images. If Steve is impressed with this I might do it, bu it hardly seems worth booting up a VPS.

Also I added a button for freezing the image so that you can easily save the image. I might eventually create a txrxlabs.org subdomain for hosting this and other projects, but for now this is all I'm doing:

<iframe src="//chriscauley.github.io/curly-vortex/" frameBorder="0" width="300" height="700"></iframe>
