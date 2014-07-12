---
layout: article
title: "响应式设计模型"
description: "虽然响应式网页设计样式正在快速发展，但能够完全兼容桌面级设备与移动设备的成熟样式却是屈指可数。"
introduction: "虽然响应式网页设计样式正在快速发展，但能够完全兼容桌面级设备与移动设备的成熟样式却是屈指可数。"
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 2
collection: multi-device-layouts
---

{% wrap content%}

{% include modules/toc.liquid %}

大多数的响应式网页设计可以归纳为五种模式：mostly fluid, column drop, layout shifter, tiny tweaks 和 off canvas。一些情况下，页面可能会采用组合设计模式，例如同时采用 column drop 与 off canvas。 这些样式最初都是由 [Luke Wroblewski](http://www.lukew.com/ff/entry.asp?1514) 定义的，他们为设计响应式式页面提供了一个坚实的基础。

### 设计模型

为了创建简洁易懂的示例，下面提到的每一个案例都是基于[`flexbox`](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Flexible_boxes)通过真实的标签创建的, 主要是在一个主 div内包含三个内容 div。 每个示例都由定义最小视图开始，并在必要的时候加入响应节点（breakpoint）。 flexbox 布局模式 能很好的支持现在的主流浏览，尽管为了最佳效果你可能需要依赖特定的前缀。

## 大体流动性模型（Mostly Fluid）

Mostly fluid 样式主要由流体式栅格（fluid grid）构成。 无论是在大尺寸或者中等大小屏幕，它都能保持尺寸不变而仅仅只是调整边距以适应更宽的屏幕。在小屏幕上，流体式栅格布局会将主要内容重新排版，使栏目垂直堆栈排列。使用流体式栅格的一个最主要优点是通常只需要在大屏幕与小屏幕之间设置一个响应点即可。

{% link_sample _code/mostly-fluid.html %}
  <img src="imgs/mostly-fluid.svg">
  试一下
{% endlink_sample %}

在最小视图的情况下，每个内容 div 垂直堆栈排列。一旦屏幕的宽度达到600px时，主容器 div 保持 width: 100%，其余的次要 div如下图所示并排排列在主 div下方。如果屏幕宽度超过了800px，主容器 div 的宽度将固定并在屏幕上居中。

使用这种设计样式的网站有：

 * [A List Apart](http://mediaqueri.es/ala/)
 * [Media Queries](http://mediaqueri.es/)
 * [SimpleBits](http://simplebits.com/)


{% include_code _code/mostly-fluid.html mfluid css %}

## 掉落列模型

对于全屏多栏目布局来说，column drop能够简单地在屏幕宽度变窄以致于容不下太多内容时自动纵向排列栏目，最终使每一个栏目都垂直堆栈排列。在这种布局样式下，响应点可以根据页面内容使用各种设计。

{% link_sample _code/column-drop.html %}
  <img src="imgs/column-drop.svg">
  试一下
{% endlink_sample %}

与 mostly fluid 的示例一样, 在最小视图中纵向垂直排列内容，但在屏幕宽度超过600px后，主要与次要内容 div占据了屏幕的全部宽度。 Div的顺序被设定为根据CSS中的order属性进行排列。 屏幕宽度为800px时，三个内容 div全部一起出现并占据了全部屏幕宽度。

使用这种设计样式的网站有：

 * [Modernizr](http://modernizr.com/)
 * [Wee Nudge](http://weenudge.com/)

{% include_code _code/column-drop.html cdrop css %}

## 活动布局模型

Layout shifter布局是响应能力最强的布局样式，它通过多个响应点来适应多种屏幕宽度。这种布局的关键在于，并不是重新排列内容或者垂直排列列而是将其四处移动。由于每个响应点对应的布局相互之间有巨大的差异，所以保持内容一致的操作更加复杂并可能涉及改动元素内部内容而不是仅仅改变全局布局。

{% link_sample _code/layout-shifter.html %}
  <img src="imgs/layout-shifter.svg">
  试一下
{% endlink_sample %}

这个简化了的示例展示了layout shifter的设计样式，在较小屏幕中的内容纵向垂直排列，但在较大的屏幕中，布局发生了很大的变化：左边是一个div而右边由两个垂直排列的div构成。

使用这种设计样式的网站有：

 * [Food Sense](http://foodsense.is/)
 * [Seminal Responsive Design
  Example](http://alistapart.com/d/responsive-web-design/ex/ex-site-FINAL.html)
 * [Andersson-Wise Architects](http://www.anderssonwise.com/)

{% include_code _code/layout-shifter.html lshifter css %}

## 微调模型

Tiny tweaks会对布局做出细微的改动，如调整字体大小，缩放图片尺寸或者微调内容位置等等。这种布局样式对于单列排版来说十分合适，比如一些单页面的长网站和含有大量文字内容的页面。


{% link_sample _code/tiny-tweaks.html %}
  <img src="imgs/tiny-tweaks.svg">
  试一下
{% endlink_sample %}


As its name implies, little changes with this sample as the screen size changes.
As the screen width gets larger, so do the font size and padding.


Sites using this pattern include:

 * [Opera's Shiny Demos](http://shinydemos.com/)
 * [Ginger Whale](http://gingerwhale.com/)
 * [Future Friendly](http://futurefriendlyweb.com/)

{% include_code _code/tiny-tweaks.html ttweaks css %}

## Off canvas

Rather than stacking content vertically, the off canvas pattern places less
frequently used content, perhaps navigation or app menus off screen, only
showing it when the screen size is large enough, and on smaller screens, content
is only a click away.

{% link_sample _code/off-canvas.html %}
  <img src="imgs/off-canvas.svg">
  试一下
{% endlink_sample %}

Rather than stacking content vertically, this sample hides two of the content
`div`s off screen by using a `transform: translate(-250px, 0)`.  JavaScript is used
to show the divs by adding an open class to the element to make visible.  As the
screen gets wider, the off-screen positioning is removed from the elements and
they're shown within the visible viewport.

Note in this sample, Safari for iOS 6 and Android Browser do not support the
`flex-flow: row nowrap` feature of `flexbox`, so we’ve had to fallback to
absolute positioning.

Sites using this pattern include:

 * [HTML5Rocks
  Articles](http://www.html5rocks.com/en/tutorials/developertools/async-call-stack/)
 * [Google Nexus](http://www.google.com/nexus/)
 * [Facebook's Mobile Site](https://m.facebook.com/)

{% include_code _code/off-canvas.html ocanvas css %}

{% include modules/nextarticle.liquid %}

{% endwrap %}
