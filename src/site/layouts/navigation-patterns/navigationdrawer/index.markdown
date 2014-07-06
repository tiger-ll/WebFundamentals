---
layout: article
title: "导航抽屉"
description: "当一个站点有着大量分类和子类的时候，导航抽屉更加合适。它可以收纳于画布元素之外，同时在全局状态中处于一个固定位置。"
thumbnail: navigationdrawer/images/navdrawer.png
article:
  written_on: 2014-01-01
  updated_on: 2014-01-06
  order: 3
rel:
  gplusauthor: https://plus.google.com/+MattGaunt
  twitterauthor: "@gauntface"
collection: navigation-patterns
introduction: "当一个站点有着大量分类和子类的时候，导航抽屉更加合适。它可以收纳于画布元素之外，同时在全局状态中处于一个固定位置。"
key-takeaways:
  navigation-drawer:
    - 你的导航抽屉对于用户来说应该可以轻松访问。
    - 如果分类过多，考虑将其分组并展开/收起组。不要让你的用户不知所措。
    - 不要将关键操作隐藏在抽屉里。像是搜索这样的功能应该永远在首页上，而不是隐藏在抽屉里。
---

{% wrap content%}

<a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/appbar-navdrawer-sample1.html">
  <img class="g-medium--full g-wide--full" src="images/navdrawer.png">
</a>

<div style="clear: both;"></div>

导航抽屉是一个主要用于展示站点导航的可滑动面板，也可以用来展示全局状态，比如用户登录情况。

用户可以通过屏幕顶端的App Bar上的目录按钮展开抽屉。

{% include modules/takeaway.liquid list=page.key-takeaways.navigation-drawer %}

这种方式的主要优点是它的内容可以在一个滚动元素内增加，能够容纳较大的网站结构，并且只占用极少的屏幕实际使用面积。

用户需要少量学习来找到导航抽屉，所以找到一个明显的地方放置目录按钮是非常重要的。

<a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/appbar-navdrawer-bottombar-sample.html">
  <img class="g--third" src="images/navdrawer-alt-1.png">
</a><a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/appbar-navdrawer-sample.html">
  <img class="g--third" src="images/navdrawer-alt-2.png">
</a><a href="{{site.baseurl}}/resources/samples/layouts/navigation-patterns/navdrawer-sample4.html">
  <img class="g--third g--last" src="images/navdrawer-alt-3.png"> 
</a>

<div style="clear: both;"></div>

### 选项卡 vs 导航抽屉

部分开发者发现当他们使用选项卡而非导航抽屉的时候，其互动率较高。

这需要在导航抽屉的灵活性和选项卡的可见性中做出权衡，你需要考虑哪种才最适合你的站点。

<div style="clear: both;"></div>

{% include modules/nextarticle.liquid %}

{% endwrap %}
