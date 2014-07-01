---
layout: article
title: "去除冗余下载"
description: "最快和最优化的资源是那些未经传送的资源。你最近有没有检查过你的资源？你不仅应该检查，而且应该定期检查，以确保所有资源都有助于传递更好的用户体验。"
introduction: "最快和最优化的资源是那些未经传送的资源。你最近有没有检查过你的资源？你不仅应该检查，而且应该定期检查，以确保所有资源都有助于传递更好的用户体验。"
article:
  written_on: 2014-04-01
  updated_on: 2014-04-29
  order: 1
collection: optimizing-content-efficiency
key-takeaways:
  eliminate-downloads:
    - "Inventory all own and third party assets on your pages"
    - "Measure the performance of each asset: its value and its technical performance"
    - "Determine if the resources are providing sufficient value"
---

{% wrap content%}

{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.eliminate-downloads %}

最快和最优化的资源是那些未经传送的资源。当然，这话听起来就像是废话，不过在实际中，这事经常被忽略：作为一个性能工程师，你的工作就是一直擦亮你的双眼，去寻找到从你的应用中去除冗余下载的机会。向你的团队质疑，或者定期重新审视那些隐性和显性的假设是一件很好的行为。比如：

* 我们总是在我们的页面上使用资源X，下载和显示它所需的消耗是否抵得上它所传达给用户的价值？我们能否测量和查验它的价值？
* 这份资源——尤其是第三方资源——是否提供了一致性能？这个资源是否在关键路径上？是否需要在关键路径上？如果这份资源在关键路径上，它是否是我们网站上的唯一故障点？比如说，如果这份资源失效了，它是否会影响到我们页面的性能和用户体验？
* 这份资源是否需要或拥有SLA？这份资源是否遵循最佳性能做法：压缩、缓存或其它？

所有在我们页面中频繁出现的资源都是不必要的，更糟糕的是，它们会阻碍页面性能，而不会为托管它们的网站或者访客带去什么价值。这点对于第一方和第三方的资源或小工具都适用：

* A站想要在首页上放一个照片轮播，这样访客就可以点一下就预览到很多照片——所有照片都是在网页加载的时候加载，用户浏览到之前
    * **问题：** 你是否计算过有多少用户在这个轮播图中看过多幅照片？你要为了下载这些大部分访客都看不到的资源而承担高昂的额外开销。
* B站想要安装一个第三方小工具来显示相关内容，用以提高社交参与或提供其他服务。
    * **问题：** 你是否跟踪过有多少访客使用这个小工具，或者点击过由这个小工具提供的内容？它所产生的参与度是否能够平衡它所消耗的开支？

正如上面所说的，尽管消除冗余下载看起来像是一句废话，在实际使用中它确实也是废话，但要做到这点，仍旧需要大量周密的思考和测量才行。事实上，为了获得最佳的效果，你应该对你页面上的每一份资源定期清查和重新审视这些问题。

{% include modules/nextarticle.liquid %}

{% endwrap %}
