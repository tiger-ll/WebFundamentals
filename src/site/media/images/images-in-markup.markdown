---
layout: article
title: "标识中的图片"
description: "其实 `img` 元素是很强大的——可以下载，解码然后渲染展示到内容区域——现代的浏览器支持一系列的图片格式。包括跨设备表现出与桌面展示一致的效果，这些仅仅需要一些细微的调整就能保证好的用户体验。"
introduction: "其实 `img` 元素是很强大的——可以下载，解码然后渲染展示到内容区域——现代的浏览器支持一系列的图片格式。包括跨设备表现出与桌面展示一致的效果，这些仅仅需要一些细微的调整就能保证好的用户体验。"
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 1
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

请记住当指明图片宽度时，为防止图片超出展示区，应使用相关联的单元。比如，'width: 50%';,将会使图片宽度达到容器元素（并非展示区或者实际像素大小）的50%大小。

由于CSS样式允许元素内容溢出该元素的容器，因此我们可能需要使用max-width：100%来防止图片或者其他内容溢出。举例来讲：

{% highlight css %}
img, embed, object, video {
  max-width: 100%;
}
{% endhighlight %}

一定要使用`img`元素的`alt`属性提供有意义的描述；这些描述能够让你的网站在屏幕阅读器以及其他辅助技术里被更好地理解。

## 使用`srcset`在高分辨率的设备上加大`img`元素的宽度

`srcset`属性能够增强`img`元素的表现效果, 让根据不同设备特性提供不同图片这一过程变得更加容易。同样，[ image-set CSS功能](#use-image-set-to-provide-high-res-images) 也行之有效, `srcset`允许浏览器根据设备特性选择最佳图片，比如在2x的展示区使用2x的图片，在带宽受限的2x展示区使用1x的图片。

{% highlight html %}
<img src="photo.png" srcset="photo@2x.png 2x" ...>
{% endhighlight %}

在不支持`srcset`的浏览器上,浏览器只会使用 `src` 属性中指定的默认图片。 这就是为什么任何时候，不管性能如何，在任何设备上我们都要保证1x的图片都可以进行展示这一做法的重要性。当`srcset`能够被支持时，以逗号分隔的图片选择条件可以被解析，让最合适的图片得以加载展示。

从像素密度到展示区宽度等种种，选择条件众多，但现在的只有像素密度被很好地支持。为在当前表现以及未来的特性间平衡，我们坚持提供2x的图片。

## 其他图片技术

### 压缩图片

[图片压缩技术](http://www.html5rocks.com/en/mobile/high-dpi/#toc-tech-overview)能够将2x的图片进行高质量压缩以适应各种设备，无论设备的实际性能怎样。基于图片类型以及压缩率，图片在变化时质量会发生变化，但图片文件大小会明显减小。

{% link_sample _code/compressive.html %}
查看示例
{% endlink_sample %}

{% include modules/remember.liquid title="Important" list=page.remember.compressive %}

### JavaScript图片替换技术

Javascript脚本图片替换技术会检测设备的性能然后“做一些恰当的事情”。你可以通过`window.devicePixelRatio`来判断设备的像素尺寸、宽高值，通过`navigator.connection`试探一些能用的网络连接，或者模拟一个请求。当这些信息被收集完毕后，你就能决定加载哪张图片了

使用Javascript这种处理方式有一个大的缺点就是这意味着在`pageload`解析器完成解析之前，图片会延迟加载。在页面加载完所有事件之前图片资源不会开始下载。并且，浏览器一般情况下会将1x和2x的图片资源都进行下载，这样导致页面变得臃肿。

{% include modules/nextarticle.liquid %}

{% endwrap %}
