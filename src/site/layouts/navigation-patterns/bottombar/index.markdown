---
layout: article
title: "底边栏"
description: "如果你正在开发一个网络应用，而且应用程序栏承载不下用户可以执行的操作总数，最好的选择就是溢出它们都塞到底边栏里。"
thumbnail: bottombar/images/bottombar.png
article:
  written_on: 2014-01-01
  updated_on: 2014-01-06
  order: 4
rel:
  gplusauthor: https://plus.google.com/+MattGaunt
  twitterauthor: "@gauntface"
collection: navigation-patterns
introduction: "如果你正在开发一个网络应用，而且应用程序栏承载不下用户可以执行的操作行为总数，最好的选择就是溢出它们都塞到底边栏里。"
key-takeaways:
  bottom-bar:
    - 只在你没有使用选项卡的时候考虑使用这种方式。
    - 最多插入5项。
    - 只有当你需要添加应用程序栏承载不下的操作时使用。
---

{% wrap content%}

<a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/bottombar-sample1.html">
  <img class="g-medium--full g-wide--full" src="images/bottombar.png">
</a>

<div style="clear: both;"></div>

我们已经知道了应用程序栏可用于放置操作行为。

对于很多站点，尤其是以内容为导向的站点来说，其空间对于相对较少的操作来说已经足够了。然而网络应用会发现他们用户界面有更多的可操作部分。

如果你没有使用选项卡，并且你需要在应用程序栏中放入太多操作，就把这些操作放在底部的栏内。

{% include modules/takeaway.liquid list=page.key-takeaways.bottom-bar %}

这么做的好处是你有更多的空间来放置操作，它们是在一个触摸友好区域，而且可以给你提供一个辅助操作区。

限制你自己最多放5个操作进去，别让那些按钮变得太小而难以触碰。

<a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/appbar-navdrawer-bottombar-sample.html">
  <img class="g--half g--last" src="images/bottom-bar-alt-1.png"> 
</a>

<div style="clear: both;"></div>

{% include modules/nextarticle.liquid %}

{% endwrap %}
