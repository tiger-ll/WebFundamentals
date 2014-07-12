---
layout: article
title: "响应式网页设计基础"
description: "绝大部分的网站并没有针对跨显示屏的浏览进行优化。通过学习这门基础课程，让你的网站无论在手机，电脑桌面或其他设备上都能被正常的浏览和使用"
introduction: "使用移动设备浏览网页的用户正以天文数字速度增长，但遗憾的是大部分的网页并没有为移动设备做出优化。移动设备通常受迫于屏幕大小的限制而采用与桌面设备不同的布局。"
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 1
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
collection: multi-device-layouts
key-takeaways:
  set-viewport:
    - 使用meta标签viewport来控制浏览器的“视口viewport。
    - 包括<code>width=device-width</code>以对应设备视窗的独立像素宽度。
    - 包括<code>initial-scale=1</code> 来建立一个CSS像素与设备独立像素的1:1关系。
    - 确认不禁用用户自我调节视窗大小功能。
  size-content-to-vp:
    - 不要使用大型固定宽度的元素。
    - 内容不应依赖于一个特定的viewport来正常展示。
    - 使用CSS media queries来应用不同的，适用于大小设备屏幕的样式。
  media-queries:
    - media queries可以根据不同设备的特性来应用不同的样式。
    - 使用 <code>min-width</code> over <code>min-device-width</code> 来保证最宽广的体验。
    - 使用相对大小数值来设定元素大小，以防打乱布局。
  choose-breakpoints:
    - 以断点为基础来创建内容，绝不可以基于特定的设备，产品以及品牌。
    - 先为最小的设备设计，然后一步一步的强化体验同时支持更多的视口大小。
    - 把每行的字数控制在70个到80个之间。
remember:
  use-commas:
    - 使用逗号","来区分属性，并能保证老版本浏览器可以合理的解析这些属性。
---
{% wrap content %}

<style>

  img.center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  video.responsiveVideo {
    width: 100%;
  }
</style>


{% include modules/toc.liquid %}

There is a multitude of different screen sizes across phones, "phablets",
tablets, desktops, game consoles, TVs, even wearables.  Screen sizes will always
be changing, so it's important that your site can adapt to any screen size,
today or in the future.

{% link_sample _code/weather.html %}
  <video autoplay loop controls class="responsiveVideo">
    <source src="videos/resize.webm" type="video/webm">
    <source src="videos/resize.mp4" type="video/mp4">
  </video>
{% endlink_sample %}

由 [Ethan Marcotte in A List Apart](http://alistapart.com/article/responsive-web-design/) 提出的自适应网页设计是为了响应使用不同设备浏览网页的用户需求。自适应网页设计要求网页的布局随着屏幕的大小与分辨率的不同而改变。例如，使用手机浏览网页的用户看到的由单列显示的内容，在平板电脑上很可能会用两列来显示相同的内容。


## 设置viewport

针对多设备浏览进行优化的网页顶部要包含一个元视口（meta viewport）元素。一个元视口标签能明白地告诉正在浏览该网页的用户如何控制页面的尺寸规格与缩放比例。

{% include modules/takeaway.liquid list=page.key-takeaways.set-viewport %}

为了提供最佳的用户体验, 移动浏览器会缩小电脑版网页的宽度（一般为980px，不同设备的缩放比例不同），并尝试通过改变字体的大小与缩放内容以在适应屏幕的同时提供尽可能好的浏览体验。 这对用户来说意味着有可能出现的文字大小并不一致，他们不得不通过双击缩放或双指缩放以获得更适于阅读的页面内容。

{% highlight html %}
<meta name="viewport" content="width=device-width, initial-scale=1.0">
{% endhighlight %}


使用元视口值 width=device-width 控制页面适应不同分辨率的屏幕宽度。无论是手机的小屏幕或桌面显示器，页面将会根据不同的屏幕尺寸重新对内容进行排版。

<div class="clear">
  <div class="g--half">
    {% link_sample _code/vp-no.html %}
      <img src="imgs/no-vp.png" srcset="imgs/no-vp.png 1x, imgs/no-vp-2x.png 2x" alt="Page without a viewport set">
      查看实例
    {% endlink_sample %}
  </div>

  <div class="g--half g--last">
    {% link_sample _code/vp.html %}
      <img src="imgs/vp.png" srcset="imgs/vp.png 1x, imgs/vp-2x.png 2x" alt="Page with a viewport set">
      查看实例
    {% endlink_sample %}
  </div>
</div>

一些浏览器在用户旋转为横向浏览的时候仅仅是保持页面宽度不变并缩放网页内容而不是对屏幕内容进行重新排版。加入属性`initial-scale=1`使页面无论在什么情况下都将CSS像素与屏幕像素的比例保持在1:1，并允许页面优先采用全尺寸屏幕宽度。


{% include modules/remember.liquid inline="True" list=page.remember.use-commas %}

### 确保viewport可用

除了设置 `initial-scale` 以外，你也可以对视口进行 `minimum-scale`, `maximum-scale` 和 `user-scalable` 等属性设置。当设置完成之后，这些属性能够禁止用户缩放视口，从而可能导致网站的可访问性问题。

## 将内容控制在viewport之内

无论是在桌面级设备或是移动设备上，用户通常会垂直滚动页面而不是水平拖拽来查看剩余内容，如果一个页面强迫用户通过水平拖拽或者缩小网页比例来查看全部网页内容的话，那么这个网站的用户体验简直糟糕透顶。

{% include modules/takeaway.liquid list=page.key-takeaways.size-content-to-vp %}

当你使用 `meta viewport` 标签来创建一个移动站点时, 很容易在无意中创建出一个并不是那么适于特定浏览视口的页面。例如一张超过视口宽度的图片将会令用户不得不水平拖拽页面以查看全图。因此你应该调整所有页面内容的大小以适应视口，避免诸如需要用户水平拖动页面此类情况的出现。

由于屏幕尺寸与CSS像素在不同的设备中存在广泛的差异（如手机与平板电脑，甚至两台不同手机之间），要完美展现页面的内容绝不能仅仅依赖于一个特定的视口宽度。

设置一个较大的绝对宽度的CSS页面元素（如下所示）将会导致 `div` 在窄屏设备视口中显得太宽（例如一台CSS像素宽度为320的iPhone）这种情况下可以使用相对宽度值，例如 `width: 100%`。同样的，使用较大的绝对定位值可能会导致页面元素落在窄屏设备的显示范围之外，在进行移动站点开发时一定要注意这一点。

<div class="clear">
  <div class="g--half">
    {% link_sample _code/vp-fixed.html %}
      <img src="imgs/vp-fixed-iph.png" srcset="imgs/vp-fixed-iph.png 1x, imgs/vp-fixed-iph-2x.png 2x"  alt="Page with a 344px fixed width element on an iPhone.">
      查看示例
    {% endlink_sample %}
  </div>

  <div class="g--half g--last">
    {% link_sample _code/vp-fixed.html %}
      <img src="imgs/vp-fixed-n5.png" srcset="imgs/vp-fixed-n5.png 1x, imgs/vp-fixed-n5-2x.png 2x"  alt="Page with a 344px fixed width element on a Nexus 5.">
      查看示例
    {% endlink_sample %}
  </div>
</div>

## 用 CSS media queries 来实现响应式

Media queries是能被运用到CSS样式的简单过滤器。使用Media queries可以轻易地改变基于设备规格所呈现的包括显示类型、宽度、高度、方向甚至分辨率在内的内容样式。

{% include modules/takeaway.liquid list=page.key-takeaways.media-queries %}


例如，你可以在print media query里定义所有需要打印的样式：

{% highlight html %}
<link rel="stylesheet" href="print.css" media="print">
{% endhighlight %}

除了在样式表链接里使用 `media` 属性以外, 还有另外两种在CSS文件里植入应用media query的方式: `@media` 和 `@import`。考虑到性能因素，相比起 `@import` 语句，前面提到的两种方式更受欢迎。

{% highlight css %}
@media print {
  /* print style sheets go here */
}

@import url(print.css) print;
{% endhighlight %}

应用在 media queries上的逻辑并不是独有的，任何符合要求的CSS块都会依据权重在CSS里优先应用。

### 根据viewport尺寸应用 media queries

Media queries 允许我们能创造一个自适应的体验，media query语句能够根据设备的规格创造规则将特定的样式应用在所有小屏幕，大屏幕以及所有中间尺寸的设备上。

{% highlight css %}
@media (query) {
  /* CSS Rules used when query matches */
}
{% endhighlight %}

在我们能定义的许多不同query中，最常用在网络设计上的还是 `min-width`, `max-width`, `min-height` 和 `max-height`.

<table class="table-2">
  <colgroup>
    <col span="1">
    <col span="1">
  </colgroup>
  <thead>
    <tr>
      <th data-th="attribute">属性</th>
      <th data-th="Result">结果</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="attribute"><code>min-width</code></td>
      <td data-th="Result">允许使用任何大于在query里定义的浏览器宽度值。</td>
    </tr>
    <tr>
      <td data-th="attribute"><code>max-width</code></td>
      <td data-th="Result">允许使用任何小于在query里定义的浏览器宽度值。</td>
    </tr>
    <tr>
      <td data-th="attribute"><code>min-height</code></td>
      <td data-th="Result">允许使用任何大于在query中定义的浏览器高度值。</td>
    </tr>
    <tr>
      <td data-th="attribute"><code>max-height</code></td>
      <td data-th="Result">允许使用任何小于在query里定义的浏览器高度值。</td>
    </tr>
    <tr>
      <td data-th="attribute"><code>orientation=portrait</code></td>
      <td data-th="Result">适用于所有高度大于等于宽度的浏览器。</td>
    </tr>
    <tr>
      <td data-th="attribute"><code>orientation=landscape</code></td>
      <td data-th="Result">适用于所有宽度大于高度的浏览器。</td>
    </tr>
  </tbody>
</table>

让我们来看一个例子：

<figure>
  {% link_sample _code/media-queries.html %}
    <img src="imgs/mq.png" class="center" srcset="imgs/mq.png 1x, imgs/mq-2x.png 2x" alt="Preview of a page using media queries to change properties as it is resized.">
  {% endlink_sample %}
</figure>

{% include_code _code/media-queries.html mqueries %}

* 当浏览器宽度在 <b>0px</b> 和 <b>640px</b> 之间时 `max-640px.css` 将被应用。
* 当浏览器宽度在 <b>500px</b> 和 <b>600px</b> 之间时, 在 `@media` 里的样式将被应用。
* 当浏览器宽度大于等于 <b>640px</b> 时 , `min-640px.css` 将被应用。
* 当浏览器 <b>宽度大于高度时</b>, `landscape.css` 将被应用。
* 当你的浏览器 <b>高度大于宽度时</b>, `portrait.css` 将被应用。


### 关于 `min-device-width` 的注释

除了 `*-width` 以外, 你也能用 `*-device-width` 创建queries; 这两者之间的差异微妙却又不可忽视。 min-width 基于浏览器窗口的大小, 而 min-device-width 则基于屏幕的尺寸，并且是**强烈不建议**的. 

在移动设备上，这两者看起来并没有太大的差别。因为大多数情况下用户并不能调整窗口的大小。但在桌面级设备上，用户希望页面的内容能够随着窗口的大小变化自动调整，使其显得更加自然。因此，你要尽量避免选用 `*-device-width`, 这样页面才能根据桌面浏览器窗口大小的变化进行调整

### 使用相对单位

自适应设计背后的重要概念，就是相对于固定宽度布局而言的流动性和比例性。 使用相对单位进行排版能帮助你简化布局并避免个别页面内容超过视口大小的情况发生。

例如，在页首的div用 width: 100% 确保div大小与视口宽度相等。div就能与屏幕完全适配，无论是在宽度为320px的iPhone，342px的黑莓Z10或是360px的Nexus 5上都不会出现过大或者过小的问题。

除此之外，相对值的应用令浏览器在根据用户的缩放比例来调整页面内容，而不再需要页面上的水平滚动条。

<div class="clear">
  <div class="g--half">
    <h2 class="text-danger text-center">NO</h2>
{% highlight css %}div.fullWidth {
  width: 320px;
  margin-left: auto;
  margin-right: auto;
}{% endhighlight %}
  </div>

  <div class="g--half g--last">
    <h2 class="text-success text-center">YES</h2>
{% highlight css %}div.fullWidth {
  width: 100%;
}{% endhighlight %}
  </div>
</div>

## 如何选择断点

人们可能会觉得根据设备的类型来定义断点是个不错的选择。温馨提示，如果你根据特定设备，产品类型，品牌名称或者操作系统来定义断点的话，后期维护将会是一场噩梦。相对的，你可以让页面内容自己决定在设备上如何布局。

{% include modules/takeaway.liquid list=page.key-takeaways.choose-breakpoints %}

### 选出主要断点：由小到大

先为适配小屏幕尺寸的内容设定断点，之后将屏幕尺寸不断扩大直至需要更多的断点。这使你优化断点并使断点始终保持最少成为可能。

让我们从下面的例子着手。这是一个天气预报，我们第一步要做的就是让天气预报在小屏幕中显得整洁美观。

<figure>
  {% link_sample _code/weather-1.html %}
    <img src="imgs/weather-1.png" class="center" srcset="imgs/weather-1.png 1x, imgs/weather-1-2x.png 2x" alt="Preview of the weather forecast displayed on a small screen.">
  {% endlink_sample %}
</figure>

接下来重新调整浏览器的尺寸，直到各个页面元素之间的空白大得影响美观。虽说这多少会受到主观因素的影响，不过600px肯定已经超出了美观的范畴。

<figure>
  {% link_sample _code/weather-1.html %}
    <img src="imgs/weather-2.png" class="center" srcset="imgs/weather-2.png 1x, imgs/weather-2-2x.png 2x" alt="Preview of the weather forecast as the page gets wider.">
  {% endlink_sample %}
</figure>

在600px处加入一个断点，创建两种新的样式表，当浏览器宽度小于等于600px时使用第一种样式表，而当浏览器宽度大于600px时选用第二种样式表。

{% include_code _code/weather-2.html mqweather2 %}

最后一步，重新构建CSS。在这个例子中，我们在 `weather.css` 中设置了一些通用的样式，如字体，图标，基本定位与颜色。为小屏幕设定的布局将放置于 `weather-small.css`，而为大屏幕设计的样式则放置在 `weather-large.css`.

<figure>
  {% link_sample _code/weather-2.html %}
    <img src="imgs/weather-3.png" class="center" srcset="imgs/weather-3.png 1x, imgs/weather-3-2x.png 2x" alt="Preview of the weather forecast designed for a wider screen.">
  {% endlink_sample %}
</figure>

### 当有必要时，定义次要断点。

除了定义主要断点以应对大幅度的布局改动之外，你也可以为一些细致的变动做出调整。例如在两个主要断点之间调整外间距与内间距或者改变字体大小，使得布局更加自然都是可行的。

首先从优化小屏幕布局着手：当视口宽度大于等于360px时加大字体，并在有足够空间的前提下，将最高温度与最低温度排列在同一行，最后将天气图标稍微放大。

{% include_code _code/weather-small.css mqsmallbpsm css %}

<div class="clear">
  <div class="g--half">
    <img src="imgs/weather-4-l.png" srcset="imgs/weather-4-l.png 1x, imgs/weather-4-l-2x.png 2x" alt="Before adding minor breakpoints.">
  </div>

  <div class="g--half g--last">
    <img src="imgs/weather-4-r.png" srcset="imgs/weather-4-r.png 1x, imgs/weather-4-r-2x.png 2x" alt="After adding minor breakpoints.">
  </div>
</div>

同样的，对大屏幕设备来说，最好对天气预报面板的最大宽度做出限制，使其不至于占据整个屏幕。

{% include_code _code/weather-large.css mqsmallbplg css %}

### 优化文本阅读体验

传统阅读观认为理想的阅读每行应有70到80个字符（约为8到10个英语单词），因此当一个文本框的宽度超过10个单词时，是时候考虑加入一个断点了。

<div class="clear">
  <div class="g-wide--1 g-medium--half">
    <img src="imgs/reading-ph.png" srcset="imgs/reading-ph.png 1x, imgs/reading-ph-2x.png 2x" alt="Before adding minor breakpoints.">
  </div>

  <div class="g-wide--3 g-wide--last g-medium--half g--last">
    <img src="imgs/reading-de.png" srcset="imgs/reading-de.png 1x, imgs/reading-de-2x.png 2x" alt="After adding minor breakpoints.">
  </div>
</div>

让我们以上图的博客为例。仔细观察你会发现，在小幕上，大小为1em的Roboto字体完美给出了每行十个词的排版，但是在较大的屏幕上，你会发现你不得不加入断点。在这种情况下,如果浏览器宽度超过575px,理想的内容宽度应该是550px。

{% include_code _code/reading.html mqreading css %}

### 不要隐藏全部的内容

在根据屏幕大小选择需要显示的内容时要考虑仔细。不要仅仅因为内容不能与屏幕适配就选择将其隐藏。是否能够适配屏幕的大小并不是衡量用户是否需要这个内容的标准。例如，从天气预报中去除花粉指数可能并不是一个好的选择，春季过敏症患者会根据这些信息来判断他们今天是否适合外出。

{% include modules/nextarticle.liquid %}

{% endwrap %}
