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

*  限制最大宽度。
*  修改元素的padding以及缩小字码。
*  使表格与标题内容float对齐。
*  使视频始终float在内容周围。
*  缩小图片大小并且让他们出现在更好的格局里面。

<div class="related-items">
<div class="related-items">
<div class="container">
<div markdown='1' class="g-wide--push-1 g-medium--push-1">
### 相关内容
{: .related-items--title}

学习更多关于Media Queries:

*  [使用Media Queries]({{site.baseurl}}/layouts/rwd-fundamentals/#use-css-media-queries-for-responsiveness)
*  [布局模式]({{site.baseurl}}/layouts/rwd-patterns/)
*  [将近流动式布局]({{site.baseurl}}/layouts/rwd-patterns/#mostly-fluid)
{: .list--links}
</div>
</div>
</div>
</div>

## 限制最大宽度。

我们只选择两个主要布局方式：一个窄viewport和一个宽viewport，两者都可以大幅度的将建立过程简单化。

同时我们也决定创建“出血”区域，这个区域无论在窄的或者宽的viewport下都会保持完全“出血”。
这意味着我们应该限制最大宽度，这样文本以及段落就不会在大型屏幕上拉伸至一行。
我们将最大值定在800px左右。

为了实现它，我们需要限制它的宽度并且将其置中。
我们需要在每个部分外层都创建一个container，并且应用"margin:auto"。
这会允许在屏幕改变大小的情况下（最大800px）内容区域保持置中。


这个container会包含一个简单的 `div` 在下面的表格当中:

{% highlight html %}<div class="container">...</div>{% endhighlight %}

{% include_code _code/fixingfirstbreakpoint.html containerhtml html %}

{% include_code _code/fixingfirstbreakpoint.html container css %}

## 修改元素的padding以及缩小字码。

在窄viewport上，我们没有很多的空间去放置内容，所以字体的大小以及粗细都会被大幅度缩小来适应屏幕。

在一个大的viewport上，我们需要考虑用户在大多数情况下都是离屏幕有一段距离的。
为了提高内容的可读性，我们可以加大或者加粗字体，或者更改padding来让选定的区域更突出。

在我们的产品页面，我们会增加区域元素之间的padding到5%。同时我们会放大每个区域的抬头。

{% include_code _code/fixingfirstbreakpoint.html padding css %}

## 使元素适应宽viewport

我们的窄viewport是一个纵向的堆积显示模式。每一个区域与其中的内容都是从上到下来显示的。

一个宽的viewport给我们很多的空间来摆放内容，保证它摆放在一个最佳位置。在我们的产品页面，根据我们的IA总结出我们可以：

*  将表格放置在抬头附近。
*  将视频放置在重点右边。
*  平铺图像。
*  扩大表格。

### Float表单元素

窄viewport意味着，我们在相比之下有很少的横向空间，来让我们随意的在屏幕上摆放元素。

来更有效的运用横向空间，我们需要打破抬头的线性流程，并且将表单与列表放在一起。

{% include_code _code/fixingfirstbreakpoint.html formfloat css %}

{% include_code _code/fixingfirstbreakpoint.html padding css %}

<video controls poster="images/floatingform.png" style="width: 100%;">
  <source src="videos/floatingform.mov" type="video/mov"></source>
  <source src="videos/floatingform.webm" type="video/webm"></source>
  <p>对不起，您的浏览器无法播放视频。
     <a href="videos/floatingform.mov">下载视频</a>.
  </p>
</video>

### Float视频元素

在窄viewport界面当中，视频的宽度是设定为屏幕的宽度，并且放置在要点列表后面。
在一个宽viewport上面，如果视频放置在要点列表后，会导致视频过度放大并且出现显示问题。

视频元素需要从窄viewport的纵向流程中移除，应该放置与内容列表对齐。

{% include_code _code/fixingfirstbreakpoint.html floatvideo css %}

### 平铺图片

在窄viewport当中（大部分为移动设备），其界面是设定为屏幕的满宽度并且纵向叠加，
这样并不会在宽viewport中正常适应。

为了让图片在宽viewport中显示正常，他们会被缩小至container宽度的30%并且横向排列（与纵向叠加对立）。
我们会添加一些border radius与box-shadow来让图片看着更漂亮一些。

<img src="images/imageswide.png" style="width:100%">

{% include_code _code/fixingfirstbreakpoint.html tileimages css %}

### 使图片与DPI相应

当使用图片的时候,
要将viewport的大小以及设备的清晰度加入考虑当中。

互联网是为了96dpi的屏幕所设计的。随着移动设备的面世，我们见证了屏幕清晰度的巨大提升，更不用提笔记本电脑的视网膜显示。
正因如此，96dpi的图片在高像素的设备上通常都看着很糟糕。

我们有一个还未完全推广的解决方案。
对于支持这个功能的浏览器，你可以在高清屏幕上显示高清图片。

{% highlight html %}
<img src="photo.png" srcset="photo@2x.png 2x">
{% endhighlight %}

<div class="related-items">
<div class="related-items">
<div class="container">
<div markdown='1' class="g-wide--push-1 g-medium--push-1">
### 相关信息
{: .related-items--title}

更多viewport的最佳实践：

* [使用srcset来实现针对高DPI设备的图片优化]({{site.baseurl}}/media/images/#enhance-imgs-with-srcset-for-high-dpi-devices)
* [使用media queries来提供高分辨率图片或者艺术指导]({{site.baseurl}}/media/images/#use-media-queries-to-provide-high-res-images-or-art-direction)
{: .list--links}

</div>
</div>
</div>
</div>

### 表格

在窄viewport的移动设备上正确显示表格并不是一件很容易的事情，要实现这个目标需要考虑特殊的需求。

在窄viewport上，我们推荐将表格分为两行，排列标题与表格单元来形成柱形图。

<video controls poster="images/responsivetable.png" style="width: 100%;">
  <source src="videos/responsivetable.mov" type="video/mov"></source>
  <source src="videos/responsivetable.webm" type="video/webm"></source>
  <p>对不起，您的浏览器无法播放视频。
     <a href="videos/responsivetable.mov">下载视频</a>.
  </p>
</video>

在我们的站点上,
我们需要为表格单独建立一个断点。
当你在为一个移动设备建造站点的时候，很难去剔除已经应用的样式，
所以我们必须把窄viewport的表格CSS文件与宽viewport区分开来。
才能有一个清晰并且统一的断点。

{% include_code _code/content-with-styles.html table-css css %}

## 结尾

**恭喜。** 当你读到这里的时候，你已经建立了你的第一个单页产品页面，这个页面会在绝大多数的移动设备上正常显示，包括适应外型以及不同的屏幕大小。

如果你有遵循这些指南，你应该已经有了一个很好的开始：

1.  创建了一个基础的IA并且在写代码之前已经对内容有一定的理解。
2.  总是设置一个viewport。
3.  在移动设备优先的前提上打造你的基础体验。
4.  在完成了移动设备体验之后，慢慢放大viewport直到结构出现问题，并且设定新的断点。
5.  重复上述步骤。

{% include modules/nextarticle.liquid %}

{% endwrap %}
