---
layout: article
title: "有效优化内容"
description: "我们的网页应用的内容、目标和功能都在不断成长 - 这样很好。然而，我们拼命地让这个网站不断丰满，却导致了另一个趋势：每个应用中的每个步骤所下载的数据总量不断上涨。为了实现优异性能，我们需要优化每一比特数据的传输过程！"
introduction: "我们的网页应用的内容、目标和功能都在不断成长 - 这样很好。然而，我们拼命地让这个网站不断丰满，却导致了另一个趋势：每个应用中的每个步骤所下载的数据总量不断上涨。为了实现优异性能，我们需要优化每一比特数据的传输过程！"
article:
  written_on: 2014-04-01
  updated_on: 2014-04-29
  order: 2
id: optimizing-content-efficiency
collection: performance
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
一个现代网页应用应该是什么样的？[HTTP Archive](http://httparchive.org/) 可以帮助我们回答这个问题。这个项目跟踪了世界上最流行的网站（从Alexa排名前一百万的网站中选取超过30万个站点），周期性检查这些网站是如何建设的，并记录、统计分析每个目标的资源数量、内容类型和元数据

<img src="images/http-archive-trends.png" class="center" alt="HTTP Archive trends">

<table>
<thead>
  <tr>
    <th></th>
    <th>第50百分位数</th>
    <th>第75百分位数</th>
    <th>第90百分位数</th>
  </tr>
</thead>
<tr>
  <td data-th="type">HTML</td>
  <td data-th="50%">13 KB</td>
  <td data-th="75%">26 KB</td>
  <td data-th="90%">54 KB</td>
</tr>
<tr>
  <td data-th="type">图片</td>
  <td data-th="50%">528 KB</td>
  <td data-th="75%">1213 KB</td>
  <td data-th="90%">2384 KB</td>
</tr>
<tr>
  <td data-th="type">JavaScript</td>
  <td data-th="50%">207 KB</td>
  <td data-th="75%">385 KB</td>
  <td data-th="90%">587 KB</td>
</tr>
<tr>
  <td data-th="type">CSS</td>
  <td data-th="50%">24 KB</td>
  <td data-th="75%">53 KB</td>
  <td data-th="90%">108 KB</td>
</tr>
<tr>
  <td data-th="type">其他</td>
  <td data-th="50%">282 KB</td>
  <td data-th="75%">308 KB</td>
  <td data-th="90%">353 KB</td>
</tr>
<tr>
  <td data-th="type"><strong>合计</strong></td>
  <td data-th="50%"><strong>1054 KB</strong></td>
  <td data-th="75%"><strong>1985 KB</strong></td>
  <td data-th="90%"><strong>3486 KB</strong></td>
</tr>
</table>

上面数据展示了2013年1月到2014年1月之间，访问网上流行的网站目标所需下载数据量的增长趋势，并不是每个网站都是按照此比率增长，也不是说每个网站都需要这么多的数据量，因此我们选了了三个不同的百分位数：第50（中位），第75和第90。

2014年初的中位网站总共需要75个请求，共计1054KB传输数据，而这个总数据（和请求数）在去年一年间一直在稳步增长。这件事本身并不令人惊讶，但是它确实带来性能上的潜在问题：是的，网速正在不断增长，但是在不同国家，其增长速率是不同的，很多用户仍旧受制于流量上限和高昂的套餐费用，这之中手机用户尤甚。

和那些电脑软件不同，网页应用并不需要一个独立的安装过程，它只需要输入RUL地址，然后我们就可以开始运行应用了——这就是网络应用的一个关键特性。**然而要想获得这种瞬间达成的效果，我们非得先获取那些加起来足有几MB的数据，然后在几百毫秒内，把这几十上百份资源集合起来才行。**

在这些要求下做出一个拥有即时性的网络体验绝非易事，这就是为什么有效优化内容如此关键了：去除不必要的下载，通过不同的压缩技术优化每份资源的传输代码，尽可能借助缓存以去掉多余的下载。

## 更多课程

{% for guide in page.articles.optimizing-content-efficiency %}
1. [{{guide.title}}]({{site.baseurl}}{{guide.url | clean}}) &mdash;
{{guide.description}}
{% endfor %}

{% endwrap %}
