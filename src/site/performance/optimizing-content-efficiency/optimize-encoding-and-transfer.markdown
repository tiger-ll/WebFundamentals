---
layout: article
title: "优化编码以及文本资源传输体积。" 
description: "我们的网页应用的内容、目标和功能都在不断成长 - 这样很好。然而，我们拼命地让这个网站不断丰满，却导致了另一个趋势：每个应用中的每个步骤所下载的数据总量不断上涨。为了实现优异性能，我们需要优化每一比特数据的传输过程！"
introduction: "我们的网页应用的内容、目标和功能都在不断成长 - 这样很好。然而，我们拼命地让这个网站不断丰满，却导致了另一个趋势：每个应用中的每个步骤所下载的数据总量不断上涨。为了实现优异性能，我们需要优化每一比特数据的传输过程！"
article:
  written_on: 2014-04-01
  updated_on: 2014-04-29
  order: 2
collection: optimizing-content-efficiency
key-takeaways:
  compression-101:
    - Compression is the process of encoding information using fewer bits
    - Eliminating unnecessary data always yields the best results
    - There are many different compression techniques and algorithms
    - You will need a variety of techniques to achieve the best compression
  minification:
    - Content-specific optimizations can significantly reduce the size of delivered resources.
    - Content-specific optimizations are best applied as part of your build/release cycle.
  text-compression:
    - "GZIP performs best on text-based assets: CSS, JavaScript, HTML"
    - All modern browsers support GZIP compression and will automatically request it
    - Your server needs to configured to enable GZIP compression
    - Some CDNs require special care to ensure that GZIP is enabled
notes:
  jquery-minify:
    - "Case in point, the uncompressed development version of the JQuery library is now approaching ~300KB. The same library, but minified (removed comments, etc.) is about 3x smaller: ~100KB."
  gzip:
    - "Believe it or not, there are cases where GZIP can increase the size of the asset. Typically, this happens when the asset is very small and the overhead of the GZIP dictionary is higher than the compression savings, or if the resource is already well compressed. Some servers allow you to specify a “minimum filesize threshold” to avoid this problem."
---

{% wrap content%}

{% include modules/toc.liquid %}

<style>
  img, video, object {
    max-width: 100%;
  }

  img.center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  pre {
    background-color: #f0f0f0;
    padding: 1em 3em;
  }
</style>

## 数据压缩第一课

一旦我们去掉了那些多余的资源，下一步就是将那些需要浏览器下载的剩余资源的总体积最小化，也就是压缩它们。资源类型不同，我们也有多种不同方式来进行处理：服务器上可运行的一般工具，特殊类型内容的预处理优化，以及需要开发者输入的资源特定优化。

需要所有这些技术的综合运用才可以实现最佳性能。

{% include modules/takeaway.liquid list=page.key-takeaways.compression-101 %}

减小数据体积的方法被称作“数据压缩”，它本身是一门深奥的学问：很多人终其一生去研究算法、技术，优化它们来提升压缩率、速度和多种压缩工具的内存消耗。无需赘言，这个话题已经超出了我们所需涉猎的范围，但是我们必须从一个高层次上去理解压缩的工作原理，以及在缩减我们的页面中各种资源的体积时，其所需的技术。

为了阐明这个过程中的核心原则，让我们来思考一下下例，要如何优化这样一个简单的文本格式的信息：

    # 下列是一份密码消息，它是由一组键值格式的头信息
    # 及其之后跟随的一个换行和一个加密信息组成。
    format: secret-cipher
    date: 04/04/14
    AAAZZBBBBEEEMMM EEETTTAAA

1. 信息有可能会包含各种注释，它们都有“#”前缀。注释不影响信息的含义或者其他表达。
1. 信息有可能会包含“头信息”，它们是一些出现在信息最前面的键值对（由“:”分隔）。
1. 信息携带文本的有效载荷。

我们能对这段目前200个字的信息做些什么，才能缩减他们的体积呢？

1. 好吧，那些注释很有意思，不过我们知道它实际上对信息的意义一点影响都没有，所以当我们传输这段信息的时候，丢掉它。
1. 有一些有效的方法可以编码头信息，我们可能可以用这些精明的技术。比如：我们不知道是不是所有的信息都有“format”和“date”，如果是的话，我们可以将其转为换为一个更短的ID，到时候只要输送ID就行了！不过我们也不能确定是不是这样，所以暂时就先这样不管它。
1. 有效载荷只有文字，而且我们不知道这段文字内容到底是啥意思（很显然，他是个“密码消息”），只看这段文字本身的话，感觉它好像是有很多荣誉。也许我们可以数一下重复字母的数量，然后更有效地编码它们，而不是传送重复的字母？
    * 比如“AAA”就可以变成“3A” - 或者有顺序的三个A。


融合我们的技术，我们可以得到下列的结果：

    format: secret-cipher
    date: 04/04/14
    3A2Z4B3E3M 3E3T3A

新的信息有56个字，这意味着我们设法将我们的信息压缩了令人感动的72%。再接再厉，考虑周全，我们这才刚刚开始！

当然也许你会问，这是挺不错的，但是它怎么帮我们优化我们的页面？我们很明显不准备发明我们自己的压缩算法，对吧？答案显而易见，我们不会，不过正如你所见，我们将会使用相同的技术，而优化我们页面中的各种资源时，也会使用相同的思考方法：预处理，特定内容优化，以及不同内容不同算法。


## 最小化：预处理和内容针对性优化

{% include modules/takeaway.liquid list=page.key-takeaways.minification %}

压缩冗余或者不必要数据的最佳方式是完全干掉它们。当然我们不能删除任何数据，但是在某些情况下，我们可能已经对特定内容的数据格式及其属性有所了解，这使得我们有可能显著减少数据的有效载荷的大小，而不影响其实际意义。

{% include_code _code/minify.html full %}

看一下上面的简单HTML页面，它里面包含了三种不同的内容类型：HTML标记，CSS样式表和JavaScript。它们各自都有不同的规则来组成有效的HTML标记、CSS规则或者Javascript内容，也都有不同的规则来指示注释内容以及其他。我们要如何减少这个页面的体积？

* 代码注释是开发者的好基友，但是浏览器不需要看到它们！只是删掉这些CSS (`/* … */`)、HTML(`<!-- … -->`)和JavaScript(`// …`)注释就可以显著减少页面的总体积。
* 一个“聪明的”CSS压缩工具能够注意到我们使用了一种没效率的方式定义‘.awesome-container’的规则，将这两个声明合并成一个并不会影响到其他的样式，却节省了更多字节。
* 空白字符（空格和制表符）在HTML、CSS和JavaScript中会对开发者提供便利。添加另一个压缩器可以去除所有的制表符和空格。

^
{% include_code _code/minified.html full %}

应用了上述几个步骤之后，我们的页面从406个字符减少到150个，63%的压缩节省！确实这样就不太好读了，不过也不用非得这样：我们可以将我们的原始页面作为“开发版”，而当我们准备将页面发布到网站的时候再应用上述步骤。

退一步看，上面的例子描述了一个重要的观点：一个通用的压缩工具——比如一个用来压缩任意文本的压缩工具——也可以把上述页面压缩得不错，不过它永远不会知道丢掉注释，合并CSS规则，或者其他几十种针对特定内容的优化方式。这就是为什么预处理/最小化/分析上下文压缩是一个如此强大的工具。

{% include modules/remember.liquid list=page.notes.jquery-minify %}

同样地，上述技术不仅适用用于文本资源。图像、视频和其他的内容类型都有它自己的元数据及有效载荷的格式。例如，当你用数码相机拍了一张照片，照片中通常也会嵌入了大量其他信息：相机设置、拍摄位置以及其他。对于你的应用来说，这些数据有可能是至关重要的（比如对于一个相片分享网站），也有可能是完全没用的，此时你就应该考虑是否值得要将它们完全去除。在实际中，这些元数据会给每个图像增加多达几十KB的体积！

简单来说，有效优化你的资源的第一步是做个清单，清单中要列出不同内容类型和你能用到怎样的特定内容优化方式来减小它们的体积——这样就能显著节省带宽！然后，当你确定了这些优化方式之后，将其加入到你的构建发布流程中，使其成为自动优化。只有这样才能保证这些优化始终有用。

## 使用GZIP压缩文本

{% include modules/takeaway.liquid list=page.key-takeaways.text-compression %}

[GZIP](http://en.wikipedia.org/wiki/Gzip)是一个可以应用在任意比特流上的通用压缩器：它运行时会记住之前见过的内容，然后会试图通过一种有效的方式查找并替换那些重复的数据碎片。如果你很好奇，可以看看 [最佳的GZIP通俗解释](https://www.youtube.com/watch?v=whGwm0Lky2s&feature=youtu.be&t=14m11s)。然而，在实际应用中，GZIP对文本内容有着最佳表现，对于大型文档来说，压缩率通常可以高达70%-90%，然而对于那些已经通过其它算法压缩过的资源（比如大部分图像格式）来说，GZIP基本上帮不上什么忙。

所有的现代浏览器都支持GZIP，并且自动对所有HTTP请求通过GZIP压缩：我们的工作是确保服务器配置正确，以便当客户端请求压缩资源时就能够提供。

<table>
<thead>
  <tr>
    <th>库</th>
    <th>体积</th>
    <th>压缩后体积</th>
    <th>压缩比例</th>
  </tr>
</thead>
<tr>
  <td data-th="library">jquery-1.11.0.js</td>
  <td data-th="size">276 KB</td>
  <td data-th="compressed">82 KB</td>
  <td data-th="savings">70%</td>
</tr>
<tr>
  <td data-th="library">jquery-1.11.0.min.js</td>
  <td data-th="size">94 KB</td>
  <td data-th="compressed">33 KB</td>
  <td data-th="savings">65%</td>
</tr>
<tr>
  <td data-th="library">angular-1.2.15.js</td>
  <td data-th="size">729 KB</td>
  <td data-th="compressed">182 KB</td>
  <td data-th="savings">75%</td>
</tr>
<tr>
  <td data-th="library">angular-1.2.15.min.js</td>
  <td data-th="size">101 KB</td>
  <td data-th="compressed">37 KB</td>
  <td data-th="savings">63%</td>
</tr>
<tr>
  <td data-th="library">bootstrap-3.1.1.css</td>
  <td data-th="size">118 KB</td>
  <td data-th="compressed">18 KB</td>
  <td data-th="savings">85%</td>
</tr>
<tr>
  <td data-th="library">bootstrap-3.1.1.min.css</td>
  <td data-th="size">98 KB</td>
  <td data-th="compressed">17 KB</td>
  <td data-th="savings">83%</td>
</tr>
<tr>
  <td data-th="library">foundation-5.css</td>
  <td data-th="size">186 KB</td>
  <td data-th="compressed">22 KB</td>
  <td data-th="savings">88%</td>
</tr>
<tr>
  <td data-th="library">foundation-5.min.css</td>
  <td data-th="size">146 KB</td>
  <td data-th="compressed">18 KB</td>
  <td data-th="savings">88%</td>
</tr>
</table>

上面的表格展现了部分目前最流行的JavaScript库和CSS框架经过GZIP压缩的成果。节省范围从60%到88%，请注意，代码最小化（在文件名中用“.min”标识）和GIZP的结合使用可以取得更好的效果。

1. **首先使用特定内容优化：CSS、JS和HTML最小化工具。**
1. **使用GZIP压缩最小化的资源。**

最好的是，GZIP是可以应用的最简单也是收益最高的压缩手段之一，可惜的是，很多人都忘了去应用它。大部分服务器会为了你的利益压缩内容，你只需要检查服务器是否配置正确，以保证它能去压缩那些可从GZIP压缩中受益的内容类型。

你的服务器的最好的配置是什么？HTML5 Boilerplate项目囊括了所有最流行的服务器[示例配置文件](https://github.com/h5bp/server-configs)，并附有每个配置和设置的详细注释：找到列表中你最喜欢的服务器，寻找GZIP部分，然后确定你的服务器按照推荐设置配置。

<img src="images/transfer-vs-actual-size.png" class="center" alt="DevTools demo of actual vs transfer size">

一个简便快捷的查看GZIP的实际作用的方式是打开Chrome开发人员工具，在网络（Network）面板中查看大小/内容（Size/Content）列：“大小”表示资源的传输大小，“内容”表示资源未经压缩时的大小。GZIP压缩使上例中的HTML资源在传输中减少了24.8KB！

{% include modules/remember.liquid list=page.notes.gzip %}

最后，再提醒一句：尽管大多数服务器在传送资源给用户的时候会自动为你压缩它们，但某些CDN会需要格外注意，并手工设置提供GZIP资源。检查你的网站并保证你的资源确确实实 [压缩](http://www.whatsmyip.org/http-compression-test/)了!



{% include modules/nextarticle.liquid %}

{% endwrap %}
