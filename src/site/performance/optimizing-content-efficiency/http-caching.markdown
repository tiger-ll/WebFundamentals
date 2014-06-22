---
layout: article
title: "HTTP缓存"
description: "通过网络获取内容是昂贵且费时的：大量的响应需要客户端与服务器之间的多次往返，这样使得浏览器可以处理那些内容的时机被延后了，另外也让访问者承担了数据消耗。因此，使用缓存和再次使用之前获取过的资源是优化性能的一个关键方向。"
introduction: "通过网络获取内容是昂贵且费时的：大量的响应需要客户端与服务器之间的多次往返，这样使得浏览器可以处理那些内容的时机被延后了，另外也让访问者承担了数据消耗。因此，使用缓存和再次使用之前获取过的资源是优化性能的一个关键方向。"
article:
  written_on: 2014-01-01
  updated_on: 2014-01-05
  order: 4
collection: optimizing-content-efficiency
key-takeaways:
  validate-etags:
    - "验证令牌（validation token）由服务器通过ETag HTTP头传达"
    - "验证令牌提供了有效的资源更新检查：如果资源没有发生更改，则不会发生数据传输。"
  cache-control:
    - "每个资源都可以通过Cache-Control HTTP头定义它的缓存策略"
    - "Cache-Control指令控制谁可以在什么情况下缓存多久响应。"
  invalidate-cache:
    - "本地缓存的响应可以在资源“过期”之前使用"
    - "在URL中嵌入文件内容指纹可以让我们强制客户端更新到响应的新版本"
    - "每个应用都需要定义自己的缓存层次结构以获得最佳性能"
notes:
  webview-cache:
    - "如果你正在你的应用中使用网络视图获取和展示网络内容，你就需要提供额外的配置标记（Configuration flag），以确定HTTP缓存已启用，并且根据你的使用情况设置合理的缓存大小，这样你的缓存才能持续。查看平台文档以确认你的设置！"
  boilerplate-configs:
    - "注意：HTML5样板文件计划收录了所有的流行服务器上的<a href='https://github.com/h5bp/server-configs'>示例配置文件</a>，并且包含了每个配置标记和设置的详细注释：在列表中找到你最喜欢的服务器，找出适当的设置，然后复制，或者确认你的服务器按照推荐的设置配置了。"
  cache-control:
    - "Cache-Control头被定义为HTTP/1.1规范的一部分，并取代了之前用于定义响应缓存策略的头信息（比如Expires）。所有的现代浏览器都支持Cache-Control，因此我们用这些就够了。"
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

好消息是所有浏览器都带有HTTP缓存实现机制！我们要做的，只是确保每个服务器响应都提供了正确的HTTP头指令，以指示浏览器可以在何时缓存多久该响应。

{% include modules/highlight.liquid character="{" position="left" title="" list=page.notes.webview-cache %}

<img src="images/http-request.png" class="center" alt="HTTP request">

当服务器返回一个响应的时候，它也发出一系列HTTP头，描述了这个响应的内容类型、长度、缓存指令、验证令牌等等。比如在上图的交换中，服务器返回了一个1024字节的响应，指示客户端缓存120秒，并提供了一个验证令牌（“x234dff”），这个令牌可以在响应过期后检查资源是否更新过)。


## 使用ETag验证缓存响应

{% include modules/takeaway.liquid list=page.key-takeaways.validate-etags %}

让我们假设在我们获取资源后的120秒，浏览器开始对相同的资源发出一个新的请求。首先，浏览器会检查本地缓存，并找到之前的响应，不幸的是这个缓存已经“过期”而无法使用了。此时，浏览器本可以简单地发出一个新的请求并获取一个新的完整的响应，不过这样就没什么效率了，因为如果资源并没有被更改过，那就没必要去重新下载原本就存在在缓存里的，一模一样的数据！

这就是ETag指定放入验证令牌所要解决的问题：服务器产生并返回一个任意的令牌，这个令牌有可能只是一段乱码，也有可能是文件内容的某种指纹。客户端不需要知道这个指纹是如何产生的，它只需要在下次请求中发送这个指纹：如果指纹仍然不变的话，就意味着资源也没有发生改变，我们就可以跳过下载过程。

<img src="images/http-cache-control.png" class="center" alt="HTTP Cache-Control example">

在上面的例子中，客户端自动在“If-None-Match（假如不匹配）”HTTP请求头中提供了ETag令牌，服务器针对当前资源检查令牌，如果没有发生更改，则返回“304 Not Modified（304未更改）”响应，以告知浏览器它缓存中所存有的这个响应并未发生更改，并可以再延长120秒。要注意我们没必要再次下载响应，这样就节约了时间和带宽。

作为一个网络开发人员，如何利用有效再验证？浏览器为我们做了很多工作：它会自动检测是否曾经指定过验证令牌，并且会在发出请求时附上找到的令牌，然后根据从服务器上收到的响应，在必要时更新缓存时间戳 **剩给我们来做的只剩下唯一一件事，那就是确认服务器真的能提供需要的ETag令牌：检查你的服务器文档中所需的配置项。**

{% include modules/remember.liquid list=page.notes.boilerplate-configs %}


## Cache-Control（缓存控制）

{% include modules/takeaway.liquid list=page.key-takeaways.cache-control %}

最佳请求就是那些不需要和服务器交流的请求：一个响应的本地副本可以让我们消灭所有的网络传输延迟，并且避免数据传输费用。为了做到这点，HTTP规范允许服务器返回[一系列不同的Cache-Control指令](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)来控制浏览器或其他中继缓存会以何种方式将该响应缓存多久。

{% include modules/remember.liquid list=page.notes.cache-control %}

<img src="images/http-cache-control-highlight.png" class="center" alt="HTTP Cache-Control example">

### "no-cache"（不缓存）与"no-store"（不保存）

“no-cache”表示对相同的URL进行后续请求时，返回的响应在未经服务器检查其是否被修改之前，不能使用。因此，如果提交一个适当的验证令牌（ETage），no-cache会增加一个往返来验证已缓存响应，但却可以在响应未发生更改的时候，避免下载。

与之相比，“no-store”就更简单了，它直接禁止浏览器和所有的中继缓存储存任何版本的返回响应——比如包含了个人隐私或者银行信息的响应。每当用户请求这个资源，都会向服务器发送一个请求，并下载到完整的响应。

### “public”（公开）vs“private”（私有）

如果某个响应被标记为“public”，那么该响应可以被缓存，即使它有与之相连的HTTP认证，甚至响应状态代码不是正常可缓存的。大多数时候，“public”不是必需的，因为显式缓存信息（像是“max-age”）就指明了该缓存是可以缓存的。

与之相对，“private”响应可以由浏览器缓存，但是通常只针对单个用户，因此不允许由任何中继缓存缓进行缓存——比如说，一个带有用户个人信息的HTML页面可以让用户浏览器缓存，但是不能让CDN缓存。

### “max-age”

这个指令指示获取到的响应，从发送请求开始以秒计算，可以重新使用的最长时间间隔——比如说“max-age=60”指示这个响应可以在接下来的60秒内缓存和重新使用。

## 定义最优Cache-Control策略

<img src="images/http-cache-decision-tree.png" class="center" alt="Cache decision tree">

根据上面的决策树来确定你应用中的特定资源或一系列资源的优化缓存策略。理想情况下，你应该尽可能长时间地在客户端缓存尽可能多的响应内容，并且为每个响应提供验证令牌来保证高效的再验证。

<table>
<thead>
  <tr>
    <th width="30%">Cache-Control指令</th>
    <th>说明</th>
  </tr>
</thead>
<tr>
  <td data-th="cache-control">max-age=86400</td>
  <td data-th="explanation">浏览器和任意中继（意即它是“public”的）可以缓存该响应，最多一天的（60秒×60分×24小时）</td>
</tr>
<tr>
  <td data-th="cache-control">private, max-age=600</td>
  <td data-th="explanation"客户端浏览器可以缓存该响应，最多10分钟（60秒×10分）</td>
</tr>
<tr>
  <td data-th="cache-control">no-store</td>
  <td data-th="explanation">禁止缓存该响应，每次请求时都必须获取完整信息。</td>
</tr>
</table>

根据HTTP Archive，基本上全球前30万（根据Alexa排名）的网站中，[近半数下载响应可以被浏览器缓存](http://httparchive.org/trends.php#maxage0)，对于重复的浏览和访问来说是个巨大的节约！当然，这并不意味着你的某个应用就要有50%的资源可供缓存：某些网站可以缓存90%以上的资源，而其他一些拥有大量私人或时间敏感的数据则根本完全不能被缓存。

**检查你的页面来识别哪些资源可以被缓存，并确保它们返回适当的Cache-Control和ETag头。**


## 作废和升级缓存响应

{% include modules/takeaway.liquid list=page.key-takeaways.invalidate-cache %}

所有由浏览器发出的HTTP请求都会先前往浏览器缓存，检查其中是否有有效缓存响应可供完成请求。如果找到了符合的，就会从缓存中读取响应，我们就可以避免由数据传输产生的网络耗时和流量消耗。 **然而，我们想升级或作废一份缓存响应的时候要怎么办？**

比如说，假如我们已经告诉访问者缓存CSS样式表24小时（max-age=86400），不过我们的设计师刚刚提交了一个想要对所有用户生效的新版。我们要如何通知所有访问者他们的缓存副本已经“过时了”，并且需要更新缓存？这是一个唬人的问题——我们做不到，至少在不改变资源URL的前提下做不到。

一旦浏览器缓存了一个响应，缓存下的版本会在它过时之前一直使用，这是由max-age或者expires决定的；抑或者是用到这些缓存因为某些原因被清除——比如用户清除了浏览器缓存。因此，当构造页面的时候，不同的用户最终可能使用了不同的文件版本；那些刚刚获取到资源的用户会使用新版本，而早先缓存过（仍旧有效的）副本的用户会在他的响应中使用老版本。

**那么我们要怎样才能两全其美：客户端缓存和快速更新？** 其实也很简单，我们可以在变更资源内容后，改变资源的URL，并强制用户下载新的响应。通常的做法，是在文件名中嵌入一个文件指纹或者版本号——比如style.**x234dff**.css。

<img src="images/http-cache-hierarchy.png" class="center" alt="Cache hierarchy">

定义每个资源缓存策略的能力允许我们定义“缓存层级”，这样我们不但可以控制每个缓存的有效时间，还可以控制用户能够多快看到新版本。举个例子，让我们分析一下上面的示例：

* HTML标记为“no-cache”，这意味着浏览器将在每次请求时，都会再验证文档，并在内容发生变动时获取最新的版本。同时，在HTML标记中，我们给CSS和JavaScript资源的URL里嵌入指纹：如果改动了那些文件，页面的HTML也会随之变化，于是将会下载HTML响应的新副本。
* CSS允许浏览器和中继缓存（比如CDN）进行缓存，其有效期为1年。注意我们可以安全使用1年这样“如此之长的有效期”，是因为我们在它的文件名中嵌入了文件的指纹：如果CSS升级了，其URL也会发生改变。
* JavaScript的有效期也设为1年，不过被标记为私有，可能是因为它包含一些不能让CDN缓存的私人用户信息。
* 图像没有版本或独有指纹，缓存有效期为1天。

ETag，Cache-Control和唯一URL，可以给我们一个皆大欢喜的方案：长期有效的时间，控制哪里可以缓存响应，以及按需升级。

## 缓存清单

没有一个固定的最佳缓存策略。根据你的流量模式、提供的数据类型，以及应用特定的数据刷新需求，你会需要定义和配置相应的资源设置，以及整体的“缓存层级”。

这里提供一些提示和技巧可以帮助你制定缓存策略：

1. **使用一致的URL：** 如果你用不同的URL提供相同的内容，那么那个内容就会被提取并保存多次。提示：注意[URL是大小写敏感的](http://www.w3.org/TR/WD-html40-970708/htmlweb.html)！
1. **保证服务器提供验证令牌（ETag）：** 当服务器上的文件未发生更改的时候，验证令牌可以使其不必传送相同的数据。
1. **定义哪些资源可以让中继缓存：** 那些所有用户用起来都一样的响应，最适合让CDN及其他中继缓存。
1. **为每个资源定义最佳缓存时间：** 不同的资源可能有不同的刷新需求。检查每个资源并为它们定义合适的max-age。
1. **为你的网站定义最佳缓存层级：** 在资源URL中包含内容指纹，以及令HTML文档拥有短时或no-chache周期，可以让你控制客户端以多快的速度获得更新。
1. **最小化代码变动（churn）：** 一些资源会比其他资源更经常升级。如果有一部分特定资源（比如JavaScript功能，或者一系列CSS样式表）需要经常更新，考虑把那些代码放到一个单独的文件里。这么做可以让剩下的内容（比如不常更新的库文件）可以从缓存中读取，这样当获取更新的时候，就可以最小化所需下载的内容。


{% include modules/nextarticle.liquid %}

{% endwrap %}
