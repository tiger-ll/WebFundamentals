---
layout: section
title: "视频"
description: "学习最简单的向网站添加视频的方法，并让用户
              在任何设备上都能享受到最佳体验。"
introduction: "用户喜欢视频；它们可以很有趣并且内容丰富。在移动设备上，视频更容易传递信息。但是视频很占带宽，而且不能在任何平台上都正常工作。用户不喜欢等待视频加载，或者当他们按下播放的时候却毫无反应。阅读更多细节来了解最简单的向网站添加视频的方法，并让用户在任何设备上都能享受到最佳体验。"
article:
  written_on: 2014-04-16
  updated_on: 2014-04-29
  order: 2
collection: introduction-to-media
id: videos
key-takeaways:
  add-a-video:
    - 在你的网站上使用video元素来加载、解码并播放视频。
    - 为你的视频创建多种格式来覆盖更多的移动平台。
    - 正确缩放你的视频，保证它们不会从容器中溢出。
    - 可访问性事宜：在video元素中添加track子元素。
remember:
  media-fragments:
    - 大多数平台都支持Media Fragments API，不过IOS不支持。
    - 确保你的服务器支持Range Requests。大部分服务器默认支持Range Requests，但是某些服务器可能会将其关闭。
  dont-overflow:
    - 不要强制设定元素大小，以免导致其长宽比与原始视频不同。拉伸或者压缩看起来都很糟糕。
  accessibility-matters:
    - 安卓Chrome、iOS Safari和除FireFox之外（参见<a href="http://caniuse.com/track" title="Track元素支持现状">caniuse.com/track</a>）的所有现有的桌面浏览器都支持track元素。也有一些可用的polyfill。我们推荐<a href='//www.delphiki.com/html5/playr/' title='Playr track element polyfill'>Playr</a>或者<a href='//captionatorjs.com/' title='Captionator track'>Captionator</a>。
  construct-video-streams:
    - 安卓的Chrome和Opera，以及IE11和桌面Chrome支持MSE，<a href='http://wiki.mozilla.org/Platform/MediaSourceExtensions' title='Firefox Media Source Extensions implementation timeline'>Firefox准备支持它</a>。
  optimize:
    - <a href="../images/">Images</a>
    - <a href="../../performance/optimizing-content-efficiency/">Optimizing content efficiency</a>
---

{% wrap content%}

<div class="media media--video">
  <iframe src="https://www.youtube.com/embed/j5fYOYrsocs?controls=2&modestbranding=1&showinfo=0" frameborder="0" allowfullscreen=""></iframe>
</div>

{% include modules/nextarticle.liquid %}

{% endwrap %}
