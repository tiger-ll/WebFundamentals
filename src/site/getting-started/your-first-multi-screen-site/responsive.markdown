---
layout: article
title: "Make it Responsive"
description: "The web is accessible on a huge range of devices from small-screen phones to huge-screen televisions. Learn how to build a site that works well across all these devices."
introduction: "The web is accessible on a huge range of devices from small-screen phones through to huge-screen televisions.  Each device presents its own unique benefits and also constraints and as a web developer you are expected to support all ranges of devices."
key-takeaways:
  make-responsive:
    - Always use a viewport 
    - Always start with a narrow viewport first and scale out
    - Base your breakpoints off when you need to adapt the content
    - Create a high-level vision of your layout across major breakpoints
notes:
  styling: 
    - We have assumed a set of styles that include color, padding and font styling that match our brand guidelines.
  not-all-at-once:
    - You don't have to move all the elements at once, you can make smaller adjustments if needed
article:
  written_on: 2014-04-17
  updated_on: 2014-04-23
  order: 2
collection: multi-screen
---

{% wrap content %}

{% include modules/toc.liquid %}

We are building a site that works across in multiple screen sizes and device
types. In the [previous
article]({{site.baseurl}}{{page.article.previous.url}}) we crafted the
Infomration Architecture of the page and created a basic structure that we
will now use to make work across all of our target screens and form-factors. 

In this guide we will take our basic structure with content and turn it in to
a beautiful page that is responsive across a large number of screen sizes.

<div class="clear">
  <figure class="g-wide--2 g-medium--half">
    <img  src="images/content.png" alt="Content" style="max-width: 100%;">
    <figcaption>{% link_sample _code/content-without-styles.html %} Content and structure {% endlink_sample %} </figcaption>
  </figure>
  <figure class="g-wide--2 g-wide--last g-medium--half g--last">
    <img  src="images/narrowsite.png" alt="Designed site" style="max-width: 100%;">
    <figcaption>{% link_sample _code/content-with-styles.html %} Final site {% endlink_sample %} </figcaption>
  </figure>
</div>

We are using the principles of Mobile First web development.  We start with a
narrow viewport &mdash; similar to a mobile phone &mdash; and build for that
experience first and start to scale up to larger device classes.  We can do 
this by making our viewport wider and making a judgment call on whether the
design and layout look right.

Earlier we created a couple of different high-level designs for how our content
should be displayed and now we need make our page adapt to those different layouts.
We do this by making a decision on where to place our breakpoints &mdash; a point
where the layout and styles change &mdash; based on how the contents fits the
screen-size.

{% include modules/takeaway.liquid title="TL;DR" list=page.key-takeaways.make-responsive %}

## Add a viewport

Even for a basic page you **must** always include a viewport meta tag.  The viewport
is the most critical component you need for building mobile-first experiences.
Without it, your site will not work well on a mobile device.

The viewport indicates to the browser that the page needs to be scaled to fit
the screen.  There are many different configurations that you can specify for
your viewport to control the display of the page.  As a default, we recommend:

{% include_code _code/viewport.html viewport %}

The viewport lives in the head of the document and only needs to be declared once.

<div class="related-items">
<div class="related-items">
<div class="container">
<div markdown='1' class="g-wide--push-1 g-medium--push-1">
### Related information
{: .related-items--title}
Learn more about the best practices of using the viewport:

*  [Setting the Viewport]({{site.baseurl}}/the-essentials/multi-device-layouts/rwd-fundamentals/index.html#set-the-viewport)
*  [Size content to the viewport]({{site.baseurl}}the-essentials/multi-device-layouts/rwd-fundamentals/index.html#size-content-to-the-viewport)
{: .list--links}

</div>
</div>
</div>
</div>

## Apply simple styling

Our product and company already has a very specific branding and font guide-lines supplied 
in a style guide.

### Style guide

A style guide is a useful way to get a high-level understanding of the visual representation 
of the page and it helps you ensure that you are consistent through out the design.

#### Colors

<div class="styles" style="font-family: monospace;">
  <div style="background-color: #39b1a4">#39b1a4</div>
  <div style="background-color: white">#ffffff</div>
  <div style="background-color: #f5f5f5">#f5f5f5</div>

  <div style="background-color: #e9e9e9">#e9e9e9</div>
  <div style="background-color: #dc4d38">#dc4d38</div>
</div>

#### Typography





### Add stylistic images

In the previous guide we added images called "content images".  These were
images that were important to the narrative of our product.  Stylistic images
are images that are not needed as part of the core content but add visual flare
or help guide the readers attention to a specific piece of content.

A good example of this is a headline image for the 'above the fold' content.  It
is often used to entice the user in to reading more about the product.

<div class="g-wide--2 g-wide--last g-medium--half g--last">
  <img  src="images/narrowsite.png" alt="Designed site" style="max-width: 100%;">
</div>

They can be very simple to include, in our case it will be the background to the 
header and we will apply it via some simple CSS.

{% highlight css %}  
#headline {
  padding: 0.8em;
  color: white;
  font-family: Roboto, sans-serif;
  background-image: url(backgroundimage.jpg);
  background-size: cover;
}
{% endhighlight %}

We have chosen a simple background image that is blurred so it doesn't take away
from the content and we have set it to `cover` the entire element that way it 
always stretches whilst maintaining the correct aspect ratio.

<br style="clear: both;">

## Set your first breakpoint

The design starts to look bad at about 600px wide.  In our case the length of
the line is going above 10 words (the optimal reading length) and that is
where we want to change it.

<video controls poster="images/firstbreakpoint.png" style="width: 100%;">
  <source src="videos/firstbreakpoint.mov" type="video/mov"></source>
  <source src="videos/firstbreakpoint.webm" type="video/webm"></source>
  <p>Sorry your browser doesn't support video. 
     <a href="videos/smiles.mov">Download the video</a>.
  </p>
</video>

600px appears to be a good place to create our first breakpoint as it will give us scope
to reposition elements to make them fit the screen better.  We can do this
using a technology called [Media Queries](/web/essentials/the-essentials
/multi-device-layouts/rwd-fundamentals/index.html#use-css-media-queries-for-
responsiveness).

{% highlight css %}
@media (min-width: 600px) {
    
}
{% endhighlight %}

There is more space on a larger screen so there is more flexibility with how
content can be displayed.

{% include modules/remember.liquid title="Note" list=page.notes.not-all-at-once %}

In the context of our product page it looks like we will
need to:

*  Constrain the maximum width of the design
*  Alter the padding of elements and reduce the text size
*  Move the form to float in-line with the heading content
*  Make the video float around the content
*  Reduce the size of the images and have them appear in a nicer grid

<div class="related-items">
<div class="related-items">
<div class="container">
<div markdown='1' class="g-wide--push-1 g-medium--push-1">
### Related information
{: .related-items--title}

Learn more about how and where to use Media Queries:

*  [Using Media Queries]({{site.baseurl}}//web/essentials/the-essentials/multi-device-layouts/rwd-fundamentals/index.html#use-css-media-queries-for-responsiveness) 
*  [Layout patterns]({{site.baseurl}}/the-essentials/multi-device-layouts/rwd-patterns/index.html) 
*  [Mostly Fluid layout]({{site.baseurl}}/the-essentials/multi-device-layouts/rwd-patterns/index.html#mostly-fluid)
{: .list--links}
</div>
</div>
</div>
</div>

## Constrain the maximum width of the design

We have chosen to have only two major layouts: a narrow viewport and a wide
viewport which greatly simplifies our build process.

We have also decided to create full-bleed sections on the narrow viewport that
stay full-bleed on the wide viewport.  This means we should constrain the
maximum width of the screen so that the text and paragraphs don't extend in to one
long single line on ultra wide screens.  We have chosen this point to be 
about 800px.

To achieve this we need to constrain the width and center the elements.  We
need  to create a container around each major section and apply a `margin:
auto`.   This will allow the screen to grow but the content remain centered
and at a maximum size of 800px.

The container will be a simple `div` in the following form:

    {% highlight html %}<div class="container">...</div>{% endhighlight %}

{% include_code _code/fixingfirstbreakpoint.html containerhtml html %}

{% include_code _code/fixingfirstbreakpoint.html container css %}

## Alter the padding and reduce text size

On the narrow viewport we don't have a lot of space to display content so
the size and weight of the typography is often drastically reduced to fit the
screen.

With a larger viewport we need to consider that the user is more likely to be
on a larger screen but further away.  To increase the readability of the
content we can increase the size and weight of the typography and we can also
alter the padding to make distinct areas stand out more.

In our product page we will increase the padding of the section elements by 
setting it to remain at 5% of the width.  We will also increase the size of
the headers for each of the sections.

{% include_code _code/fixingfirstbreakpoint.html padding css %}

## Adapt elements to wide viewport

Our narrow viewport was a stacked linear display.  Each major section and the content
inside them was displayed in order from top to bottom.

A wide viewport gives us extra space to use to display the content in an optimal way
for that screen.  For our product page this means that according to our IA we can:

*  move the form around the header information
*  position the video to the right of the key points
*  tile the images
*  expand the table.

### Float the Form element

The narrow viewport means that we have a lot less horizontal space available for
us to comfortably position elements on the screen.

To make more effective use of the horizontal screen space we need to break out
of the  the linear flow of the header and move the form and the list to be next
to each other.

{% include_code _code/fixingfirstbreakpoint.html formfloat css %}

{% include_code _code/fixingfirstbreakpoint.html padding css %}

<video controls poster="images/floatingform.png" style="width: 100%;">
  <source src="videos/floatingform.mov" type="video/mov"></source>
  <source src="videos/floatingform.webm" type="video/webm"></source>
  <p>Sorry your browser doesn't support video. 
     <a href="videos/floatingform.mov">Download the video</a>.
  </p>
</video>

### Float the Video element

The video in the narrow viewport interface is designed  be  the full width of
the screen and positioned after the list of key features.  On a wide viewport
the  video will scale up to be too large and not look correct when placed next
to our list of features.

The video element needs to be moved out of the vertical flow of the narrow
viewport and should be display side by side with the bulleted list of content.


{% include_code _code/fixingfirstbreakpoint.html floatvideo css %}

<video controls poster="images/floatingvideo.png" style="width: 100%;">
  <source src="videos/floatingvideo.mov" type="video/mov"></source>
  <source src="videos/floatingvideo.webm" type="video/webm"></source>
  <p>Sorry your browser doesn't support video. 
     <a href="videos/floatingvideo.mov">Download the video</a>.
  </p>
</video>

### Tile the Images

The images in the narrow viewport (mobile devices mostly) interface are set to
be  the full width of the screen and stacked vertically.  This doesn't scale
well on a wide viewport.

To make the images look correct on the screen they are scaled to 50% of the
container width.  This means that we will get a nice grid of images and the
images will inflate to large.

{% include_code _code/fixingfirstbreakpoint.html tileimages css %}

Tiling images is a good idea because it allows you to display content more 
effectively depending on the size of the viewport.

<video controls poster="images/tileimages.png" style="width: 100%;">
  <source src="videos/tileimages.mov" type="video/mov"></source>
  <source src="videos/tileimages.webm" type="video/webm"></source>
  <p>Sorry your browser doesn't support video. 
     <a href="videos/tileimages.mov">Download the video</a>.
  </p>
</video>

### Make images responsive to DPI

When using images a web developer now also needs to take not only the size of
the viewport in to consideration but the density of the display.

The web was built for 96dpi screens.  With the introduction of mobile devices
we have seen a huge increase in the pixel density of screens not to mention
Retina class displays on laptops.  As such, images that are encoded to 96dpi
often look terrible on a hi-dpi device.

We have a solution that is not widely adopted yet but for browsers that
support it let you display a high density image on a high density display.

{% highlight html %}
<img src="photo.png" srcset="photo@2x.png 2x" />  
{% endhighlight %}

<div class="related-items">
<div class="related-items">
<div class="container">
<div markdown='1' class="g-wide--push-1 g-medium--push-1">
### Related information
{: .related-items--title}

Learn how to effectively use images for varying screen densities:

* [Enhance img’s with srcset for high DPI devices]({{site.baseurl}}/the-essentials/introduction-to-media/images/index.html#enhance-imgs-with-srcset-for-high-dpi-devices)
* [Use media queries to provide high res images or art direction]({{site.baseurl}}/the-essentials/introduction-to-media/images/index.html#use-media-queries-to-provide-high-res-images-or-art-direction)
{: .list--links}

</div>
</div>
</div>
</div>

### Tables

Tables are very hard to get right on devices that have a narrow viewport and need
special consideration.

<video controls poster="images/responsivetable.png" style="width: 100%;">
  <source src="videos/responsivetable.mov" type="video/mov"></source>
  <source src="videos/responsivetable.webm" type="video/webm"></source>
  <p>Sorry your browser doesn't support video. 
     <a href="videos/responsivetable.mov">Download the video</a>.
  </p>
</video>

<div class="related-items">
<div class="related-items">
<div class="container">
<div markdown='1' class="g-wide--push-1 g-medium--push-1">
### Related information
{: .related-items--title}

*  Link to images
*  Link to responsive images.
*  Link to videos
</div>
</div>
</div>
</div>


## Wrapping up

**CONGRATULATIONS.** By the time you read this you will have created your
first simple product landing page that works across a large range of devices,
form-factors and screen sizes.

If you follow these guidelines you will be off to a good start:

1.  Create a basic IA and understand your content before you code.
2.  Always set a viewport
3.  Create your base experience around mobile-first approach
4.  Once you have your mobile experience, increase the width of the display 
   until it doesn't look right and set your breakpoint there.
5.  Keep iterating.

{% include modules/nextarticle.liquid %}

{% endwrap %}