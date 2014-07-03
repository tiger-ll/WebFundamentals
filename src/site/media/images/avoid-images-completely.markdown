---
layout: article
title: "完全避免图片"
description: "有些时候，最佳的图形展示可能压根就不是一张图片。只要有可能，我们建议使用本地浏览器来实现相近的功能或效果。"
introduction: "有些时候，最佳的图形展示可能压根就不是一张图片。只要有可能，我们建议使用本地浏览器来实现相近的功能或效果。浏览器可以预先加载图片然后进行图形渲染。这表示浏览器不再需要进行单独的图片资源下载并过滤变形的图片。我们可以使用字符编码或者字体图标表现图标"
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 3
collection: images
key-takeaways:
  use-right-image:
    - Use the best image for the characteristics of the display, consider
      screen size, device resolution and page layout.
    - Change the <code>background-image</code> property in CSS for high DPI
      displays using media queries with <code>min-resolution</code> and
      <code>-webkit-min-device-pixel-ratio</code>.
    - Use srcset to provide high resolution images in addition to the 1x
      image in markup.
    - Consider the performance costs when using JavaScript image replacement
      techniques or when serving highly compressed high resolution images to
      lower resolution devices.
  avoid-images:
    - Avoid images whenever possible, instead, leverage browser capabilities,
      use unicode characters in place of images, and replace complex icons
      with icon fonts.
  optimize-images:
    - Don't just randomly choose an image format, understand the different
      formats available, and use the format best suited.
    - Include image optimization and compression tools into your workflow to
      reduce file sizes.
    - Reduce the number of http requests by placing frequently used images
      into image sprites.
    - Consider loading images only after they’ve scrolled into view to
      improve the initial page load time and reduce the initial page weight.
remember:
  compressive:
    - Use caution with the compressive technique because of the increased
      memory and decoding costs it requires.  Resizing large images to fit on
      smaller screens is expensive and can be particularly painful on low-end
      devices where both memory and processing is limited.
related:
  optimize:
    - <a href="../../performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html#image-optimization">Image optimization</a>
    - <a href="../../performance/optimizing-content-efficiency/">Optimizing content efficiency</a>
---

{% wrap content%}

<style>
  img, video, object {
    max-width: 100%;
  }

  img.center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
</style>

{% include modules/toc.liquid %}


{% include modules/takeaway.liquid list=page.key-takeaways.avoid-images %}

## 在标识中放置文字，取代嵌入图片

网页的任何地方如果是文字，就使用文字而不是嵌入图片，例如在标题中使用图片，将电话号码或者地址之类的联系信息直接放在图片里。这些可以防止他人对这些信息进行复制粘贴加以利用，让信息不会被屏幕阅读器读取，不会响应式变化。作为替换，你可以在你的标记里使用文字，必要时使用网络字体实现你需要的风格。

## 使用CSS替换图片

现代浏览器使用CSS特性来创建样式，这将预先需要加载图片。举例来说，复杂的渐变可以运用<code>background</code>属性来生成，阴影可以运用 <code>box-shadow</code>生成，圆角可以运用<code>border-radius</code>属性加到元素上。

<style>
  p#noImage {
    margin-top: 2em;
    padding: 1em;
    padding-bottom: 2em;
    color: white;
    border-radius: 5px;
    box-shadow: 5px 5px 4px 0 rgba(9,130,154,0.2);
    background: linear-gradient(rgba(9, 130, 154, 1), rgba(9, 130, 154, 0.5));
  }
  
  p#noImage code {
    color: rgb(64, 64, 64);
  }
</style>
<p id="noImage">
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque sit 
amet augue eu magna scelerisque porta ut ut dolor. Nullam placerat egestas 
nisl sed sollicitudin. Fusce placerat, ipsum ac vestibulum porta, purus 
dolor mollis nunc, pharetra vehicula nulla nunc quis elit. Duis ornare 
fringilla dui non vehicula. In hac habitasse platea dictumst. Donec 
ipsum lectus, hendrerit malesuada sapien eget, venenatis tempus purus.
</p>

{% highlight html %}
<style>
  div#noImage {
    color: white;
    border-radius: 5px;
    box-shadow: 5px 5px 4px 0 rgba(9,130,154,0.2);
    background: linear-gradient(rgba(9, 130, 154, 1), rgba(9, 130, 154, 0.5));
  }
</style>
{% endhighlight %}

记住使用这些技术并不需要呈现周期，一种对手机意义非凡的技术。如果用得过了，你会因此损失一些你已取得的效果并妨碍表现性能。

## 使用字符编码替换简单的图标

许多字体里包含并支持非常多的符号编码，这些可以用来替换图片。不像图片，字符编码能很好地进行缩放，并且不管展示屏多大或多小它们都看起来很不错。

除了普通字符集，字符码也包含了数字符号 (&#8528;)， 箭头 (&#8592;)， 数学运算符 (&#8730;)，几何图形
(&#9733;),控制符号 (&#9654;)，盲文点字模型 (&#10255;)，音乐符号 (&#9836;)，希腊字母( (&#937;)，甚至国际象棋符号 (&#9822;)。

这种包含编码字符相同方法已经实现，实体命名为：`&#XXXX`，`XXXX` 表示字符编码号。举例说明：

{% highlight html %}
你是一个超级巨&#9733;
{% endhighlight %}

你是一个超级巨&#9733;

## 使用图标字体代替复杂图标

为了适应更多复杂的图标需要，图标字体普遍变得轻量级，在单一的HTTP请求中很易用。图标文字相较于图片来说有许多优势

* 它们是矢量图形可以被无限缩放。
* CSS样式控制颜色、阴影、透明度以及简单动画。
* 一整套的图标可以在一个字体里下载。

{% link_sample _code/icon-font.html %}
<img src="img/icon-fonts.png" class="center"
srcset="img/icon-fonts.png 1x, img/icon-fonts-2x.png 2x"
alt="Example of a page that uses FontAwesome for it's font icons.">
{% endlink_sample %}
{% include_code _code/icon-font.html iconfont html %}

有成百上千的免费和付费图标字体可用，包括[Font
Awesome](http://fortawesome.github.io/Font-Awesome/),
[Pictos](http://pictos.cc/) and [Glyphicons](http://glyphicons.com/).

一定要保证平衡额外的HTTP请求和图标文件大小的权重。例如，如果你只是需要少量的图标，你最好使用一张图片或者一个图片的子画面。

{% include modules/nextarticle.liquid %}

{% endwrap %}
