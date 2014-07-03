---
layout: article
title: "CSS中的图片"
description: "为元素使用复杂的图片时，CSS样式中的`background`属性十分强大，能让图片重复甚至更多。当该属性与media queries联合使用时，能基于屏幕分辨率、展示区大小或者其他为设备加载最合适的图片。"
introduction: "为元素使用复杂的图片时，CSS样式中的`background`属性十分强大，能让图片重复甚至更多。当该属性与media queries联合使用时，能基于屏幕分辨率、展示区大小或者其他为设备加载最合适的图片。"
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 2
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

{% include modules/takeaway.liquid list=page.key-takeaways.use-right-image %}

## 使用media queries来加载条件响应的图片或者艺术指导。

Media queries（设备查询）不仅仅影响页面布局，也用来根据视窗宽度对应加载图片，或者提供艺术指导。

用以下的示例进行说明， 在较小的屏幕上，只有`small.png`会被加载放入到`div`元素中, 在较大的屏幕上时, `background-image: url(body.png)`会被加载到body元素上并且`background-image: url(large.png)`被加载到内容div元素中。

{% include_code _code/conditional-mq.html conditional css %}

## 使用image-set提供高分辨率图片

在CSS样式中使用`image-set()`提高`background`属性的表现能力, 让不同的设备特性选择不同的图片变得更加容易。这允许浏览器根据设备特性选择最佳图片，例如在2x的展示区使用2x的图片，或者在一个带宽受限的2x的设备上使用1x的图片。

{% highlight css %}
background-image: image-set(
  url(icon1x.jpg) 1x,
  url(icon2x.jpg) 2x
);
{% endhighlight %}

加载合适的图片后，浏览器将图片进行相应的缩放。换句话说，浏览器假定2x的图片有两倍的1x的图片尺寸，并将2x的图片以2作为基数进行等比例缩小，这样图片就能在页面上等大呈现。

浏览器对`image-set()`的支持仍处于发展中，现在只有以`-webkit`作为渲染内核的Chrome浏览器和Safari浏览器对该属性进行支持。 我们必须考虑当浏览器无法支持`image-set()`属性时我们应该有备用的图片，举例说明：

{% include_code _code/image-set.html imageset css %}

以上将合适的资源加载到支持image-set的浏览器，否则以1x的大小进行内容加载。重点提示当浏览器对`image-set()`的支持比较低时，大多数的浏览器都将会加载1x的资源。

## 使用media queries提供高分辨率图片或者艺术指导

多媒体查询将基于[设备像素比](http://www.html5rocks.com/en/mobile/high-dpi/#toc-bg)进行规则定义, 使将不同尺寸的图片进行1x或者2x展示变得更加容易。

{% highlight css %}
@media (min-resolution: 2dppx),
(-webkit-min-device-pixel-ratio: 2)
{
  /* High dpi styles & resources here */
}
{% endhighlight %}

Chrome, Firefox以及Opera都支持 `(min-resolution: 2dppx)`标准, 但Safari以及Android 浏览器需要提供不带`dppx`前缀的旧式语法的代理。请记住这些样式只有当设备符合多媒体查询条件时才会得以展示，你必须写好基本样式。这样也能够保证当浏览器不支持多媒体查询分辨率特性时，一些内容仍然可以被渲染展示。

{% include_code _code/media-query-dppx.html mqdppx css %}

你也可以根据展示区大小使用min-width来进行不同大小的图片。这项技术的好处在于，当多媒体查询不符合时图片不会被加载。举例来讲，只有在浏览器宽度在500像素以上时，图片文件`bg.png`才会被加载到`body`元素上。

{% highlight css %}
@media (min-width: 500px) {
  body {
    background-image: url(bg.png);
  }
}
{% endhighlight %}

{% include modules/nextarticle.liquid %}

{% endwrap %}
