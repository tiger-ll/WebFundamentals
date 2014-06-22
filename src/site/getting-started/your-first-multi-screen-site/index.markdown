---
layout: default
title: "你的第一个多画面结构网站"
description: "互联网是大多数设备都可以访问的，不管是手机还是大型屏幕。在这里你可以学到如何去建立一个在每一个设备上都可以很好的运行的网站。"
article:
  written_on: 2014-01-01
  updated_on: 2014-01-06
  order: 2
id: multi-screen
collection: getting-started
lessonsToc: false
---

<div class="article-container">
  <div class="editorial-header">
    <div class="container">
      <div class="content">

        <h1>开始</h1>
        <h2>{{ page.title }}</h2>

        <p class="editorial-header__excerpt">{{page.description}}</p>

      </div>
    </div>
  </div>
</div>

{% wrap content%}

建立一个多画面结构的体验并不像听着一样困难. 在这个课题当中, 我们会一步一步的建立一个产品介绍页面, 这个页面是为了推广我们的 
[CS256移动网络开发教程](https://www.udacity.com/course/cs256)，这个页面会在每个设备上都可以运作正常.

## 最终作品

在你完成上面那些教程之后, 你就已经做出了一个相当出色的产品页面,并可以运用在任何一个你自己的网站上. 
这个页面会是响应式的, 支持的范围小至手机大至电视都没有问题.

<figure class="demo clear">
  <img class="g-wide--1 g-medium--half" src="images/narrowsite.jpg" alt="Narrow Viewport final look">
  <img  class="g-wide--3 g-wide--last g-medium--half g--last" src="images/widesite.jpg" alt="Narrow Viewport final look">
</figure>

{% endwrap %}


<div class="container-medium">
  <div class="next-lessons next-lessons--minimal" data-current-lesson="03">
    <h3><i class="icon icon-lessons"></i> 课程</h3>
<div markdown="1">
{% for guide in page.articles.multi-screen %}
1. [{{guide.title}}]({{site.baseurl}}{{guide.url | clean}}) &mdash;
{{guide.description}}
{% endfor %}
</div>
  </div>
</div>


