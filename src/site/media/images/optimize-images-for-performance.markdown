---
layout: article
title: "优化图片表现"
description: "图片通常占了大多数的下载字节，也常占据了大部分的页面视觉空间。因此，优化图片通常可以为你的页面带来最大的字节存储以及性能改进。"
introduction: "图片通常占了大多数的下载字节，也常占据了大部分的页面视觉空间。因此，优化图片通常可以为你的页面带来最大的字节存储以及性能改进：浏览器下载更少的字节，更少与其他用户间的带宽竞争，以及更快的浏览器加载并显示所有资源。"
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 4
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

{% wrap content %}

{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.optimize-images %}

## 选择正确的格式

有两种类型的图像可以考虑：[矢量图](http://en.wikipedia.org/wiki/Vector_graphics)以及[位图](http://en.wikipedia.org/wiki/Raster_graphics)。就位图而言，你也需要选择适当的格式，比如：`GIF`、 `PNG`、 `JPG`。

**位图**，就像照片或者其他图片，图像由占据网格的一个个像素点构成。代表性的位图，比如来自照相机或者扫描仪，或者可以在浏览器canvas元素中创建。 图像的尺寸越大，文件大小随之越大。当缩放的比例大于原始尺寸是，位图会因为浏览器需要猜测丢失的像素点儿产生模糊。

**矢量图**, 如标志和艺术线条，都由一系列的曲线、直线、形状以及填补色构成。矢量图项目通常由 Illustrator或者Inkscape创建并且保存为矢量格式比如[`SVG`](http://css-tricks.com/using-svg/)。 因为矢量图由简单的基本元构成，它们可以被无失真的放大并且不改变文件大小。

当选择合适的格式时，考虑两种图像的原始类型（位图还是矢量图）以及内容（颜色、、动画、文字等）都非常重要。没有哪一种格式能够适用所有的图片类型并且每一种格式都有自己的优缺点。

选择正确的图片格式，从这些指导开始入手

* 对照片类图片采用`JPG`格式。
* 对标志或者线稿这类矢量艺术图以及纯色图形采用`SVG`格式。如果矢量图格式不支持，尝试一下WebP或者PNG格式。
* 使用PNG格式而不是`GIF`格式因为`PNG`格式允许更多的颜色并提供更好的压缩率。
* 对于较长的动画，考虑使用`<video>`标签以提供更好的图像质量并允许用户控制回放。

## 减少文件大小

图片文件大小可以考虑当保存完毕使用“后处理”来减小大小。有很多的工具可以用于压缩图片——失真以及不失真的、线上的、用户界面式的、命令行式的。只要有可能，最好采用图片的自动优化，这样它就能成为你工作流中的一等公民。

一些工具能对`JPG`以及`PNG`格式的文件进一步无失真地压缩，不影响图片质量。对`JPG`格式，使用 [jpegtran](http://jpegclub.org/)或者[jpegoptim](http://freshmeat.net/projects/jpegoptim/)（仅适用于Linux；运行-strip-all选项）。对`PNG`格式，使用[OptiPNG](http://optipng.sourceforge.net/)或者[PNGOUT](http://www.advsys.net/ken/util/pngout.htm)。

## 使用image sprites技术

CSS spriting是将一定数量的图片合并放在一张“sprite sheet”图片里的技术。个人可以通过指明偏移量来使用图片中的正确的那部分。

{% link_sample _code/image-sprite.html %}
<img src="img/sprite-sheet.png" class="center" alt="Image sprite sheet used in example">
{% endlink_sample %}
{% include_code _code/image-sprite.html sprite css %}

Image sprites的优势是在加载多个图片时，可以减少下载请求数，同时允许缓存。

## 考虑延迟加载

延迟加载可以显著加快长页面的加载，仅当必要或者主要内容完成加载渲染时，才加载页面下方包含的图片部分。除了改进性能，使用延迟加载能够创建无限滚动的用户体验。

创建无限滚动加载的页面时需要小心，因为内容加载后是可见的，搜索引擎或许永远不看内容。除此以外，希望在页脚寻找信息用户可能永远看不到页脚内容，因为一直在被加载新内容。

{% include modules/related.liquid list=page.related.optimize %}

{% include modules/nextarticle.liquid %}

{% endwrap %}