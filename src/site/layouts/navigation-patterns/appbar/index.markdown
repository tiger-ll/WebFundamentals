---
layout: article
title: "应用程序栏"
description: "用户已经习惯于在网页版站点寻找页头，但在移动设备上，你应该使用应用程序栏来代替。"
thumbnail: appbar/images/appbar.png
article:
  written_on: 2014-01-01
  updated_on: 2014-01-06
  order: 1
rel:
  gplusauthor: https://plus.google.com/+MattGaunt
collection: navigation-patterns
introduction: "用户已经习惯于在网页版站点寻找页头，但在移动设备上，你应该使用应用程序栏来代替。"
key-takeaways:
  app-bar:
    - 你的标志应该展示在每一屏的顶端，并且可以使用户回到你的首页。
    - 如果你有一个菜单按钮，把它放在应用程序栏的最左边或者最右边，并且保证在全站中，它一直在相同的位置。
    - 你页面中的关键行为应一直在应用程序栏上。
---

{% wrap content%}

<a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/appbar-navdrawer-sample1.html">
  <img class="g-medium--full g-wide--full" src="images/appbar.png">
</a>

<div style="clear: both;"></div>

用户会理所当然地觉得，当他登录你的网站的时候，你的网站标志会永远在页面顶端，而点击它就能跳转到你的首页上。

一般而言网站会有页面头部来完成这个工作。在移动设备上则使用应用程序栏。

{% include modules/takeaway.liquid list=page.key-takeaways.app-bar %}

应用程序栏包含三个元素。

- 你的网站标志
- 基本操作
- （可选）菜单按钮

几乎网上的每个网站都会有让他们的用户来执行的行为，比如说搜索。在应用程序栏上放置按钮来执行这些行为，让你的用户下意识地去找到当前页面可行的行为都有哪些。

如果你有一个菜单，使用汉堡包图标（三条横线），然后把它放在最左边或者最右边。如果你选好了一边，就不要移动它了，保证它一直处在同一个位置，这样用户只需记住一次它在哪。

## 左边 vs 右边的菜单按钮

如果你的菜单有滑动，你就要选择把菜单放在左边还是右边。

用户通常会认为左上角是最重要的UI元素，然而那里也是单手持握手机时最难碰到的地方。放在右上角也会使它显得突出和重要，同时单手持我手机时也比较容易点到。

<a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/appbar-navdrawer-sample1.html">
  <img class="g--half" src="images/appbar-menu-left.png">
</a>
<a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/appbar-navdrawer-sample2.html">
  <img class="g--half g--last" src="images/appbar-menu-right.png">
</a>

<div style="clear: both;"></div>

## 指导

应用程序栏是一系列基本原则，你应该使用它来为你的用户提供可预见的经验，不过仍有很多机会在其样式、按钮和交互方式上创新。

<a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/appbar-navdrawer-bottombar-sample.html">
  <img class="g--half" src="images/appbar-alt-1.png">
</a>
<a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/appbar-navdrawer-sample.html">
  <img class="g--half g--last" src="images/appbar-alt-2.png">
</a>

<div style="clear: both;"></div>

{% include modules/nextarticle.liquid %}

{% endwrap %}
