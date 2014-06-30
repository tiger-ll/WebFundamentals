---
layout: article
title: "响应式设计"
description: "互联网是大多数设备都可以访问的，不管是手机还是大型屏幕。在这里你可以学到如何去建立一个在每一个设备上都可以很好的运行的网站。"
introduction: "互联网是大多数设备都可以访问的，不管是手机还是大型屏幕。每一个设备都有自身的优点以及限制。而作为一个网络开发者，支持所有设备是职责之一。"
key-takeaways:
  make-responsive:
    - Always use a viewport.
    - Always start with a narrow viewport first and scale out.
    - Base your breakpoints off when you need to adapt the content.
    - Create a high-level vision of your layout across major breakpoints.
notes:
  styling:
    - We have assumed a set of styles that include color, padding and font styling that match our brand guidelines.
  not-all-at-once:
    - You don't have to move all the elements at once, you can make smaller adjustments if needed.
article:
  written_on: 2014-04-17
  updated_on: 2014-04-23
  order: 2
collection: multi-screen
---

{% wrap content %}

{% include modules/toc.liquid %}
我们正在建立一个跨设备并且跨屏幕的网站。在[上一课当中]({{site.baseurl}}{{page.article.previous.url}}), 我们建立了各个页面的内容框架以及基本的结构。在这个教程当中，我们会把我们的框架与内容结合到一起来建立一个漂亮的页面，这个页面会在绝大多数的设备上都会是响应式的。

<div class="clear">
  <figure class="g-wide--2 g-medium--half">
    <img  src="images/content.png" alt="Content" style="max-width: 100%;">
    <figcaption>{% link_sample _code/content-without-styles.html %} 内容与结构 {% endlink_sample %} </figcaption>
  </figure>
  <figure class="g-wide--2 g-wide--last g-medium--half g--last">
    <img  src="images/narrowsite.png" alt="Designed site" style="max-width: 100%;">
    <figcaption>{% link_sample _code/content-with-styles.html %} 最终结果 {% endlink_sample %} </figcaption>
  </figure>
</div>

遵循移动网络开发的原则，
我们从一个很窄的viewport &mdash; 跟手机很相似 &mdash;
我们先从手机开始。
然后再一步一步的扩展到更大的设备。
我们可以逐步扩大viewport同时决定设计和布局是否合适来实现。

刚刚我们为我们的内容制作了两个高水准的设计。现在我们要让我们的页面去适应不同的布局。
我们通过放置断点&mdash;决定结构以及样式&mdash;断点的位置取决于内容如何适应窗口大小。

{% include modules/takeaway.liquid list=page.key-takeaways.make-responsive %}

## 添加一个viewport
就算是一个非常基础的页面，你 **必须** 一直包括一个viewport meta标签。
在建立跨设备体验的过程当中，viewport是最重要的一部分。
没有它，你的站点不会在一个移动设备上正常运转。

Viewport决定设备浏览器如何决定窗口是否需要适应网页。有很多设置都可以通过指定viewport来调控页面如何显示。
我们推荐：

{% include_code _code/viewport.html viewport %}

Viewport的配置只会出现在head当中，并且只需要声明一次。

<div class="related-items">
<div class="related-items">
<div class="container">
<div markdown='1' class="g-wide--push-1 g-medium--push-1">
### 相关信息
{: .related-items--title}
学习更多使用viewport的最佳实践：
*  [设定Viewport]({{site.baseurl}}/layouts/rwd-fundamentals/#set-the-viewport)
*  [将内容控制在viewport当中]({{site.baseurl}}/layouts/rwd-fundamentals/#size-content-to-the-viewport)
{: .list--links}

</div>
</div>
</div>
</div>

## 应用简单的样式

我们的公司与产品已经有一个非常详细的品牌推广以及字体使用指南，包含在我们的样式指南当中。

### 样式指南

样式指南是一个非常强大的工具，用来帮助读者对于样式的展现有一个更高层次的理解。并且有助于保持设计的一致性。

#### 色彩

<div class="styles" style="font-family: monospace;">
  <div style="background-color: #39b1a4">#39b1a4</div>
  <div style="background-color: white">#ffffff</div>
  <div style="background-color: #f5f5f5">#f5f5f5</div>

  <div style="background-color: #e9e9e9">#e9e9e9</div>
  <div style="background-color: #dc4d38">#dc4d38</div>
</div>

### 添加样式型图片

在上一个指南当中，我们添加了一些“内容图片”。这些图片的重要性在于介绍产品。
样式型图片不是像“内容图像“那样的核心元素，但是可以为页面添加一些视觉元素，
来引导用户的注意力到选定的内容区域。

其中很好的例子就是用一个标题图片来吸引用户来阅读更多关于产品的内容

<div class="g-wide--2 g-wide--last g-medium--half g--last">
  <img  src="images/narrowsite.png" alt="Designed site" style="max-width: 100%;">
</div>

添加这个元素可以很简单的做到。在我们的案例当中，它将会是header的背景图片，我们会给它应用一些简单的CSS。

{% highlight css %}
#headline {
  padding: 0.8em;
  color: white;
  font-family: Roboto, sans-serif;
  background-image: url(backgroundimage.jpg);
  background-size: cover;
}
{% endhighlight %}

我们选择了一个非常简单的背景图片并且应用了一点虚化效果，用来防止用户的注意力被转移。
并且我们将它设置为"cover"，它的作用就是使该元素会在保持原比例上自由拉伸。

<br style="clear: both;">

## 设置你的第一个断点

这个设计在600px的时候开始出现显示问题。在我们这个案例中，
每一行文字都有超过10个单词的长度（最佳阅读长度），
这就是我们要更改的地方。

<video controls poster="images/firstbreakpoint.png" style="width: 100%;">
  <source src="videos/firstbreakpoint.mov" type="video/mov"></source>
  <source src="videos/firstbreakpoint.webm" type="video/webm"></source>
  <p>Sorry your browser doesn't support video.
     <a href="videos/firstbreakpoint.mov">Download the video</a>.
  </p>
</video>

600px似乎是一个很好的出发点，它会给我们一个范围来规划元素的位置。我们可以通过一个技术叫做
[Media Queries]({{site.baseurl}}/layouts/rwd-fundamentals/#use-css-media-queries-for-responsiveness)。

{% highlight css %}
@media (min-width: 600px) {

}
{% endhighlight %}

在一个更大的显示设备上，可以更灵活的来布局内容。

{% include modules/remember.liquid title="Note" list=page.notes.not-all-at-once %}

在我们的产品页面当中，看起来我们需要做：

*  Constrain the maximum width of the design.
*  Alter the padding of elements and reduce the text size.
*  Move the form to float in-line with the heading content.
*  Make the video float around the content.
*  Reduce the size of the images and have them appear in a nicer grid.

<div class="related-items">
<div class="related-items">
<div class="container">
<div markdown='1' class="g-wide--push-1 g-medium--push-1">
### Related information
{: .related-items--title}

Learn more about how and where to use Media Queries:

*  [Using Media Queries]({{site.baseurl}}/layouts/rwd-fundamentals/#use-css-media-queries-for-responsiveness)
*  [Layout patterns]({{site.baseurl}}/layouts/rwd-patterns/)
*  [Mostly Fluid layout]({{site.baseurl}}/layouts/rwd-patterns/#mostly-fluid)
{: .list--links}
</div>
</div>
</div>
</div>

## Constrain the maximum width of the design

We have chosen to have only two major layouts: a narrow viewport and a wide
viewport, which greatly simplifies our build process.

We have also decided to create full-bleed sections on the narrow viewport that
stay full-bleed on the wide viewport.  This means we should constrain the
maximum width of the screen so that the text and paragraphs don't extend into one
long, single line on ultra-wide screens.  We have chosen this point to be
about 800px.

To achieve this, we need to constrain the width and center the elements.  We
need  to create a container around each major section and apply a `margin:
auto`.  This will allow the screen to grow but the content remain centered
and at a maximum size of 800px.

The container will be a simple `div` in the following form:

{% highlight html %}<div class="container">...</div>{% endhighlight %}

{% include_code _code/fixingfirstbreakpoint.html containerhtml html %}

{% include_code _code/fixingfirstbreakpoint.html container css %}

## Alter the padding and reduce text size

On the narrow viewport, we don't have a lot of space to display content so
the size and weight of the typography is often drastically reduced to fit the
screen.

With a larger viewport, we need to consider that the user is more likely to be
on a larger screen but further away.  To increase the readability of the
content, we can increase the size and weight of the typography and we can also
alter the padding to make distinct areas stand out more.

In our product page, we will increase the padding of the section elements by
setting it to remain at 5% of the width.  We will also increase the size of
the headers for each of the sections.

{% include_code _code/fixingfirstbreakpoint.html padding css %}

## Adapt elements to wide viewport

Our narrow viewport was a stacked linear display.  Each major section and the content
inside them was displayed in order from top to bottom.

A wide viewport gives us extra space to use to display the content in an optimal way
for that screen.  For our product page, this means that according to our IA we can:

*  Move the form around the header information.
*  Position the video to the right of the key points.
*  Tile the images.
*  Expand the table.

### Float the Form element

The narrow viewport means that we have a lot less horizontal space available for
us to comfortably position elements on the screen.

To make more effective use of the horizontal screen space, we need to break out
of the  the linear flow of the header and move the form and list to be next
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

The video in the narrow viewport interface is designed  to be the full width of
the screen and positioned after the list of key features. On a wide viewport,
the video will scale up to be too large and look incorrect when placed next
to our list of features.

The video element needs to be moved out of the vertical flow of the narrow
viewport and should be displayed side-by-side with the bulleted list of content.

{% include_code _code/fixingfirstbreakpoint.html floatvideo css %}

### Tile the Images

The images in the narrow viewport (mobile devices mostly) interface are set to
be  the full width of the screen and stacked vertically.  This doesn't scale
well on a wide viewport.

To make the images look correct on the a wide viewport, they are scaled to 30%
of the container width and laid out horizontally (rather than vertically in
the narrow view). We will also add some border radius and box-shadow to make
the images look more appealing.

<img src="images/imageswide.png" style="width:100%">

{% include_code _code/fixingfirstbreakpoint.html tileimages css %}

### Make images responsive to DPI

When using images,
take the size of the viewport and the density of the display into consideration.

The web was built for 96dpi screens.  With the introduction of mobile devices,
we have seen a huge increase in the pixel density of screens not to mention
Retina class displays on laptops.  As such, images that are encoded to 96dpi
often look terrible on a hi-dpi device.

We have a solution that is not widely adopted yet.
For browsers that support it, you can display a high density image on a high density display.

{% highlight html %}
<img src="photo.png" srcset="photo@2x.png 2x">
{% endhighlight %}

<div class="related-items">
<div class="related-items">
<div class="container">
<div markdown='1' class="g-wide--push-1 g-medium--push-1">
### Related information
{: .related-items--title}

Learn how to effectively use images for varying screen densities:

* [Enhance imgs with srcset for high DPI devices]({{site.baseurl}}/media/images/#enhance-imgs-with-srcset-for-high-dpi-devices)
* [Use media queries to provide high res images or art direction]({{site.baseurl}}/media/images/#use-media-queries-to-provide-high-res-images-or-art-direction)
{: .list--links}

</div>
</div>
</div>
</div>

### Tables

Tables are very hard to get right on devices that have a narrow viewport and need
special consideration.

We recommend on a narrow viewport that you make your table into two rows,
transposing the heading and cells in a row to make the columnar.

<video controls poster="images/responsivetable.png" style="width: 100%;">
  <source src="videos/responsivetable.mov" type="video/mov"></source>
  <source src="videos/responsivetable.webm" type="video/webm"></source>
  <p>Sorry your browser doesn't support video.
     <a href="videos/responsivetable.mov">Download the video</a>.
  </p>
</video>

In our site,
we had to create an extra breakpoint just for the table content.
When you build for a mobile device first, it is harder to undo applied styles,
so we must section off the narrow viewport table CSS from the wide viewport css.
This gives us a clear and consistent break.

{% include_code _code/content-with-styles.html table-css css %}

## Wrapping up

**CONGRATULATIONS.** By the time you read this, you will have created your
first simple product landing page that works across a large range of devices,
form-factors, and screen sizes.

If you follow these guidelines, you will be off to a good start:

1.  Create a basic IA and understand your content before you code.
2.  Always set a viewport.
3.  Create your base experience around mobile-first approach.
4.  Once you have your mobile experience, increase the width of the display
   until it doesn't look right and set your breakpoint there.
5.  Keep iterating.

{% include modules/nextarticle.liquid %}

{% endwrap %}
