---
layout: article
title: "图片"
description: "一幅图片胜过1000个单词，每个页面里图片都是一个主要部分。但它们也是需要加载的主要部分。响应式网络设计不仅能让我们的布局基于设备特性，也能够基于图片产生变化。"
introduction: "一幅图片胜过1000个单词，每个页面里图片都是一个主要部分。但它们也是需要加载的主要部分。响应式网络设计不仅能让我们的布局基于设备特性，也能够基于图片产生变化。"
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 1
collection: introduction-to-media
id: images
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

### 响应式图片

响应式的网络设计不仅仅意味着我们的布局能够基于设备特性产生变化，网页内容也要随之改变。举例来讲，在高分辨率（2x）显示下，高分辨率的图表需要保证清晰度。在浏览器宽度为800像素时，一张宽度设置为50%图片展示效果可能只是马马虎虎，但在宽度较窄的手机上它会占据太多空间，并在适应更小尺寸屏幕时依然会占据同样大的带宽。

### 艺术指导

<img class="center" src="img/art-direction.png" alt="Art direction example"
srcset="img/art-direction.png 1x, img/art-direction-2x.png 2x">

在另一些情况下图片可能需要大幅度的变化：改变比例、裁剪甚至整张替换。在这些情况下，改变图片通常涉及到艺术指导。参阅[responsiveimages.org/demos/](http://responsiveimages.org/demos/) 查看更多示例。

{% for guide in page.articles.images %}
1. [{{guide.title}}]({{site.baseurl}}{{guide.url | clean}}) &mdash;
{{guide.description}}
{% endfor %}

{% include modules/nextarticle.liquid %}

{% endwrap %}
