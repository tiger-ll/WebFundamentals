---
layout: article
title: "图像优化"
description: "图像通常是网页中需要下载字节最多的部分，并且通常占据着一些重要的视觉空间。因此，优化图像通常可以为你的网站带来最大量的数据节省和性能提升：浏览器需要下载的数据量越少，客户端的带宽压力就越小，并且浏览器可以下载并在屏幕内渲染有效内容的速度越快。"
introduction: "图像通常是网页中需要下载字节最多的部分，并且通常占据着一些重要的视觉空间。因此，优化图像通常可以为你的网站带来最大量的数据节省和性能提升：浏览器需要下载的数据量越少，客户端的带宽压力就越小，并且浏览器可以下载并在屏幕内渲染有效内容的速度越快。"
article:
  written_on: 2014-05-07
  updated_on: 2014-05-10
  order: 3
collection: optimizing-content-efficiency
key-takeaways:
  replace:
    - 去掉无用的图像资源
    - 尽可能利用CSS3特效
    - 使用网络字体（web font）而不是在图像内写字
  vector-raster:
    - 矢量图像是那些几何形状图像的最理想图像
    - 矢量图像可以放大缩小，并且与屏幕分辨率无关
    - 位图应该用在哪些有着大量不规则形状和细节的复杂场景中
  hidpi:
    - 高分辨率屏幕的每个CSS像素中包含多个设备像素
    - 高分辨率图像需要明显更多的像素和字节
    - 图像优化技术是一样的，和分辨率无关
  optimizing-vector:
    - SVG是一种基于XML的图像格式
    - SVG文件应该最小化以减少体积
    - SVG文件应该使用GZIP压缩
  optimizing-raster:
    - 位图是个像素网格
    - 每个像素包含颜色和透明度信息
    - 图像压缩使用多种技术来减少每个像素所需的字节数，以减少图像的体积
  lossless-lossy:
    - 基于我们眼睛的工作原理，图像是有损压缩的最佳候选
    - 图像优化是有损和无损压缩的功能
    - 不同的图像格式的差异在于哪些有损及无损算法是如何应用于优化图像上的
    - '对于所有图像而言，没有一种最好的格式或者“质量设定”：每个特定压缩手段及图像内容的集合都会导致独特的输出'
  formats:
    - "从选择正确的通用格式开始：GIF、PNG、JPEG"
    - "体验并选择每种格式的最佳设定：质量、色板等等"
    - 考虑为现代客户端加入WebP和JPEG XR资源
  scaled-images:
    - 提供不同尺寸的资源是最简单并且有效的优化方式之一
    - 密切关注那些巨大的资源，因为它们需要高开支
    - 通过缩小你的图像为展示尺寸来减少无用的像素数


notes:
  decompressed:
    - "顺便一提，不用关心从服务器传送到客户端的图像格式所使用的数据，当图像在浏览器中解码的时候，每个像素永远占据4字节内存。这对于大型图像和内存紧缺的设备来说是一个重要限制——比如低端移动设备。"
  artifacts:
    - "从左到右（PNG）：32位（16M色），7位（128色），5位（32色）。带有颜色变化的复杂场合（渐变、天空等等），往往需要更大的色板才能够避免像是5位资源中的像素化的天空，这种视觉上的不自然感。另一方面，如果图像只用到了少数几种颜色，那一个大色板就只是浪费宝贵的比特而已！"
  quality:
    - "要注意不同图像格式的质量水平并不能直接比较，因为用于编码图像的算法不同：90质量的JPEG和90质量的WebP的效果完全不同。事实上，就算是相同图像格式，因压缩工具的使用，其质量水平也有可能导致输出结果在视觉上的显著差异！"
  resized:
    - '鼠标悬停在图像元素上，Chrome开发工具就会显示图像资源的“原始”和“显示”尺寸。在上述例子中，下载的图像尺寸是300x260像素的，但是在客户端中却是缩小到245x212展示的。'
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

图像优化既是一门艺术也是一门科学：说艺术是因为对于如何最佳压缩特定图像，并没有一个确定的答案，而说其科学是因为现在已经有了很多成熟的技术和算法来显著减少图像体积。为你的图像寻找最佳方案需要仔细分析很多方面：格式性能、编码内容、质量、像素面积以及其他。

## 去除和替换图像

{% include modules/takeaway.liquid list=page.key-takeaways.replace %}

你应该自问的首要问题是，一个图像是否能够呈现你所追求的效果。好的设计是简单的，而且能产生最好的性能。如果你能减少一个图像资源，减少这个和页面中的HTML、CSS、Javascript及其它资源相比巨大的多的资源，那么这就是永恒的最佳策略。也就是说，一个合适的图片也可以传递超过千字的信息，所以应该由你来决定并找到这个平衡点。

然后，你应该考虑是否有其它更有效的，可以实现预期效果的替代技术：

* **CSS效果** （渐变、投影等等）和CSS动画可以用于创建在不同分辨率和缩放情况下都边缘清晰的与分辨率无关的资源，通常只要一个图像文件所需字节的一小部分。
* **网络字体** 保证了使用好看的字体的同时，维持了选择、搜索和缩放文字的能力，这在可用性上是一个显著的提升。

如果你发现你曾经在图像资源里编入文字，别这么干了再好好想想。好的字体对于好设计、品牌推广和可读性来说都至关重要，但图中字只能传递很烂的用户体验：文字无法选中、无法搜索、无法缩放、无法获取、对高分辨率设备不友好。使用网络字体需要它[自身的优化系统](https://www.igvita.com/2014/01/31/optimizing-web-font-rendering-performance/)，但它解决了所有这些担忧，并且成为显示文字的更好选择。


## 矢量 vs. 位图

{% include modules/takeaway.liquid list=page.key-takeaways.vector-raster %}

一旦你决定了图像是真正能达到预期效果的最佳格式，接下来的关键抉择就是选择一个合适的格式：

&nbsp;

<div class="clear">
  <div class="g--half">
    <b>矢量图</b>
    <img class="center" src="images/vector-zoom.png" alt="Zoomed-in vector image">
  </div>

  <div class="g--half g--last">
    <b>位图</b>
    <img src="images/raster-zoom.png" alt="Zoomed-in raster image">
  </div>
</div>

* [矢量图](http://en.wikipedia.org/wiki/Vector_graphics)使用线、点和多边形来展现一个图像。
* [位图](http://en.wikipedia.org/wiki/Raster_graphics) 是在矩阵网格中编写入每一个像素的信息来展现图像。

每个格式都有它自己的优缺点。矢量图非常适合那些由简单几何图形（比如LOGO、文字之类的）组成的内容，在任何分辨率和缩放设置下都能保持清晰，因此它是高分辨率屏幕，以及需要在多种尺寸下展示的资源的理想格式。

然而，矢量格式在复杂场景（比如一张照片）中就不行了：用于描述所有形状的SVG标签总量会惊人的多，而且其输出的图像可能仍然无法“像照片一样真实”。在这种情况下，你就应该使用一种位图格式，比如GIF、PNG、JPEG，或者像是JPEG-XR和WebP这种更新的格式。

位图没有那么好的分辨率及单独缩放特性，当你放大一个位图的时候，你会看到锯齿和模糊的图形。因此你需要保存多个版本的位图以适应不同分辨率，才能传达最优的用户体验。


## 高分辨率屏幕的影响

{% include modules/takeaway.liquid list=page.key-takeaways.hidpi %}

当我们说道图像像素的时候，我们需要分清两种不同概念的像素：CSS像素和设备像素。一个CCS像素可能包含多个设备像素——因为，一个CSS像素可能与设备像素一一对应，也可能由多个设备像素显示。重点呢？其实是这样，设备像素越多，屏幕显示的内容细节就更好。

<img src="images/css-vs-device-pixels.png" class="center" alt="CSS vs device pixels">

高分辨率（HiDPI）屏幕看上去很美好，但是有一个明显的权衡：我们的图像资源需要更多细节，才能显示出更多设备像素的优势。好消息是，作为可以在任何分辨率下都渲染出清晰边缘的矢量图，是完成这个任务的理想人选。我们可能需要承担更多的处理消耗来渲染更好的细节，不过其基础资源是一样的，并且与分辨率无关。

另一方面，位图要面临更大的挑战，因为它们的图像数据是以单个像素为基础编码的。因此图像像素越多，位图文件体积越大。举个例子，我们来看下一个照片资源在100x100（CSS）像素下的不同之处：

<table class="table-3">
<colgroup><col span="1"><col span="1"><col span="1"></colgroup>
<thead>
  <tr>
    <th>屏幕分辨率</th>
    <th>总像素数</th>
    <th>未经压缩的文件大小（4字节1像素）</th>
  </tr>
</thead>
<tbody>
<tr>
  <td data-th="resolution">1x</td>
  <td data-th="total pixels">100 x 100 = 10,000</td>
  <td data-th="filesize">40,000 字节</td>
</tr>
<tr>
  <td data-th="resolution">2x</td>
  <td data-th="total pixels">100 x 100 x 4 = 40,000</td>
  <td data-th="filesize">160,000 字节</td>
</tr>
<tr>
  <td data-th="resolution">3x</td>
  <td data-th="total pixels">100 x 100 x 9 = 90,000</td>
  <td data-th="filesize">360,000 字节</td>
</tr>
</tbody>
</table>

当我们加倍物理屏幕的分辨率的时候，像素总数增长到原来的四倍：加倍水平像素，垂直像素也会随之倍增。因此，一个“2x”屏幕所需像素数量并不是两倍，而是四倍！

所以这在应用中有什么意义？高分辨率屏幕能够让我们展现更好看的图像，这是一个伟大的产品特性。然而，高分辨率屏幕也需要高分辨率的图像：鉴于矢量图是与分辨率无关并且可以永远清晰的，尽量用它，如果需要一张位图，请优化每一张图的多个变量——继续阅读以下内容，了解更多细节。


## 优化矢量图

{% include modules/takeaway.liquid list=page.key-takeaways.optimizing-vector %}

所有现代浏览器都支持可缩放矢量图形（SVG），它是基于XML的用于描述二维图形的图像格式：我们可以直接在页面中嵌入SVG标记，也可以作为一个外部资源。反过来看，大部分矢量绘图软甲都可以生成SVG文件，或者直接在你喜欢的文本编辑器中手写。

{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
<!-- Generator: Adobe Illustrator 17.1.0, SVG Export Plug-In . SVG Version: 6.00 Build 0)  -->
<svg version="1.2" baseProfile="tiny" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
   x="0px" y="0px" viewBox="0 0 612 792" xml:space="preserve">
<g id="XMLID_1_">
  <g>
    <circle fill="red" stroke="black" stroke-width="2" stroke-miterlimit="10" cx="50" cy="50" r="40"/>
  </g>
</g>
</svg>
{% endhighlight %}

上面的例子会渲染出一个红色黑边的简单圆形，这是由Adobe Illustrator生成的。如你所见，它包含很多元数据，像是图层信息、注释以及XML命名空间这些，在浏览器中渲染的时候通常是不需要的。因此使用诸如[svgo](https://github.com/svg/svgo)这样的工具来最小化你的SVG文件永远是个好主意。

譬如说，svgo可以将上面的由Illustrator生成的SVG文件减小58%，从470字节减小到199字节。更进一步说，SVG作为基于XML的格式，可以让我们使用GZIP压缩技术来减小其传输体积——确定你的服务器设置可以压缩SVG资源！


## 优化位图

{% include modules/takeaway.liquid list=page.key-takeaways.optimizing-raster %}

一个位图就是一个简单的由单个“像素”组成的二维网格——比如一个100x100像素的图像就是一个10,000像素的序列。而每个像素都存储为“[RGBA](http://en.wikipedia.org/wiki/RGBA_color_space)”值：（R）红通道，（G）绿通道，（B）通道和（A）阿尔法（透明度）通道。

在内部，浏览器给每个通道分配256个值（色调），每个通道被转换为8比特，每个像素4字节（4通道 x 8比特 = 32比特 = 4字节）。因此，如果我们知道网格的大小，我们就可以轻易算出文件大小：

* 100 x 100px 图像由 10,000 个像素组成
* 10,000 pixels x 4 bytes = 40,000 bytes
* 40,000 bytes / 1024 = 39 KB

^

{% include modules/remember.liquid title="Note" list=page.notes.decompressed %}

<table class="table-3">
<colgroup><col span="1"><col span="1"><col span="1"></colgroup>
<thead>
  <tr>
    <th>尺寸</th>
    <th>像素数</th>
    <th>文件尺寸</th>
  </tr>
</thead>
<tbody>
<tr>
  <td data-th="dimensions">100 x 100</td>
  <td data-th="pixels">10,000</td>
  <td data-th="file size">39 KB</td>
</tr>
<tr>
  <td data-th="dimensions">200 x 200</td>
  <td data-th="pixels">40,000</td>
  <td data-th="file size">156 KB</td>
</tr>
<tr>
  <td data-th="dimensions">300 x 300</td>
  <td data-th="pixels">90,000</td>
  <td data-th="file size">351 KB</td>
</tr>
<tr>
  <td data-th="dimensions">500 x 500</td>
  <td data-th="pixels">250,000</td>
  <td data-th="file size">977 KB</td>
</tr>
<tr>
  <td data-th="dimensions">800 x 800</td>
  <td data-th="pixels">640,000</td>
  <td data-th="file size">2500 KB</td>
</tr>
</tbody>
</table>

39KB for a 100x100像素的图像有39KB看起来似乎不是什么大问题，不过更大的图像的文件体积就会呈爆炸式增长，下载图片就变得又慢又昂贵。谢天谢地，我们迄今为止讨论的都是“未经压缩的”图像格式。我们要做点什么才能减小图像文件体积呢？

一个简单的办法是减小图像的“位深”（bit-depth），从每个通道8比特减小到一个更小的色板：每个通道8比特可以为我们提供每个通道256个值，共计16,777,216（2563）色。如果我们将其减少到256色？那么我们的RGB通道总共只需要8比特，而且可以立即保存为每像素2字节——将我们原始的每像素4字节格式压缩节省了50%！

<img src="images/artifacts.png" class="center" alt="Compression artifacts">

{% include modules/remember.liquid title="Note" list=page.notes.artifacts %}

接下来，当我们优化了单个像素中的存储数据，我们可以更聪明点也看看它附近的像素：结果发现，很多图片，尤其是照片，很多临近的像素都有相似的颜色——比如说天空、重复的纹理等等。利用这个信息，我们的压缩工具可以应用“[差分编码](http://en.wikipedia.org/wiki/Delta_encoding)”来避免储存每单个像素的值，我们可以只储存其附近像素的值差：如果临近的像素都是一样的，那么其差值就是0，那么我们只要储存一个比特就好了！不过为什么就此打住呢…

人眼对不同颜色有着不同的敏感度：我们可以通过在色板中增加或减少这些颜色，来优化我们的颜色编码以解决这个问题。
“附近”像素组成一个二维网格，这意味着每个像素都有多个友邻：我们可以利用这个事实来进一步提升差分编码。
除了每个像素的紧邻，我们还可以扫视更大范围的像素块，并且为不同的块使用不同的编码设置。等等等等不一而足…

如你所见，图像优化很快就变得复杂起来（或者说有趣起来，看各人的观点了），并且成为了学术和商业研究的活跃领域。图像占据了大量字节，因而开发更好的图像压缩技术具有极高的价值！如果你有兴趣了解更多信息，可以参看[维基百科条目](http://en.wikipedia.org/wiki/Image_compression)，或者查看[WebP压缩技术白皮书](https://developers.google.com/speed/webp/docs/compression)作为实训案例。

所以，再次重申，这些都很伟大，但也很学术：它是如何帮助我们优化页面上的图像？我们绝不是处在一个发明新压缩技术的位置上，但是我们需要了解问题的形状：RGBA像素、位深还有多种优化技术。所有这些概念都是至关重要的，需要在我们深入讨论不同位图图像格式之前理解并牢记。


## 无损 vs 有损图像压缩

{% include modules/takeaway.liquid list=page.key-takeaways.lossless-lossy %}

对于特定类型的数据，像是页面的源代码，或者一个可执行文件，其关键的一点是压缩工具不会改变或损失原始信息：遗漏或误记任何一比特数据都有可能完全改变文件内容的含义，或者更糟糕的，完全损坏它。对于另外一些类型的数据，比如图像、音频和视频，也许非常适合原始数据的“近似”表达。

事实上，根据眼睛的工作原理，我们通常可以舍弃每个像素的部分信息来减少图像的文件体积——比如我们的眼睛对于不同颜色有不同的敏感度，这意味着我们可以使用更少的比特来编码部分颜色。其结果是，一个典型的图像优化路径包括两个主要步骤：

1. 通过舍弃部分像素数据，使用“[有损](http://en.wikipedia.org/wiki/Lossy_compression)”滤镜处理图像
1. 通过压缩像素数据，使用“[无损](http://en.wikipedia.org/wiki/Lossless_compression)”滤镜处理图像

**第一个步骤是可选的，其具体算法也根据图像格式而定，不过重要的是需要理解，所有图片都可以经过有损压缩步骤来减少其文件体积。** 事实上，诸如GIF、PNG、JPEG这些不同图像格式之间的区别，就是在有损和无损步骤的时候，其使用（或舍弃）的特定算法的组合。

那么，“最佳的”有损及无损优化配置是什么？其答案取决于图像内容和你自己的标准，比如文件大小和有损压缩导致的压缩痕迹之间的取舍：在某些情况下，你可能想要跳过有损优化来确保完全不失真的复杂细节，在另一些情况下，你可能会积极使用有损压缩来减小图片资源的文件体积。这需要你自己的判断，以及需要应用的环境——从来没有一个通用的设置。

<img src="images/save-for-web.png" class="center" alt="保存为web所用格式">

作为一个实际应用的例子，当我们使用像是JPEG这样的有损格式，压缩工具通常会显示一个自定的“质量”设置（比如在Adobe Photoshop中“保存为web所用格式”功能中所提供的质量滑块），通常是个从1到100的数值，它控制着有损及无损算法的组合方式。为了取得最佳效果，为你的图像尝试各种不同的质量设置，不要担心下调质量——其视觉效果通常会非常好，同时节约相当多的文件体积。

{% include modules/remember.liquid title="Note" list=page.notes.quality %}


## 选择正确的图像格式

{% include modules/takeaway.liquid list=page.key-takeaways.formats %}

除了不同的有损及无损压缩算法，不同的图像格式也提供不同的特性，比如动画和透明度（阿尔法）通道。因此，对特定图像“正确格式”的选择，是视觉效果和功能需求的组合。


<table class="table-4">
<colgroup><col span="1"><col span="1"><col span="1"><col span="1"></colgroup>
<thead>
  <tr>
    <th>格式</th>
    <th>透明度</th>
    <th>动画</th>
    <th>浏览器</th>
  </tr>
</thead>
<tbody>
<tr>
  <td data-th="format"><a href="http://en.wikipedia.org/wiki/Graphics_Interchange_Format">GIF</a></td>
  <td data-th="transparency">是</td>
  <td data-th="animation">是</td>
  <td data-th="browser">全部</td>
</tr>
<tr>
  <td data-th="format"><a href="http://en.wikipedia.org/wiki/Portable_Network_Graphics">PNG</a></td>
  <td data-th="transparency">是</td>
  <td data-th="animation">否</td>
  <td data-th="browser">全部</td>
</tr>
<tr>
  <td data-th="format"><a href="http://en.wikipedia.org/wiki/JPEG">JPEG</a></td>
  <td data-th="transparency">否</td>
  <td data-th="animation">否</td>
  <td data-th="browser">全部</td>
</tr>
<tr>
  <td data-th="format"><a href="http://en.wikipedia.org/wiki/JPEG_XR">JPEG XR</a></td>
  <td data-th="transparency">全部</td>
  <td data-th="animation">全部</td>
  <td data-th="browser">IE</td>
</tr>
<tr>
  <td data-th="format"><a href="http://en.wikipedia.org/wiki/WebP">WebP</a></td>
  <td data-th="transparency">是</td>
  <td data-th="animation">是</td>
  <td data-th="browser">Chrome, Opera, Android</td>
</tr>
</tbody>
</table>

现在一共有3种广泛使用的图像格式：GIF、PNG和JPEG。除了这些格式，部分浏览器也支持更新的格式，比如WebP和JPEG XP，这些格式可以提供更好的全局压缩和更多特性。所以你应该用哪种格式呢？

<img src="images/format-tree.png" class="center" alt="Save for web">

1. **你是否需要动画？如果是，GIF是唯一的通用选择。**
  * GIF限制色板最多为256色，这对于大部分图像来说是个不咋样的选择。更进一步说，PNG-8拥有更好的压缩率和更小的色板。因此，只有当你需要动画的时候，GIF才是最好的选择。
1. **你是否需要在高分辨率下拥有更好的细节？使用PNG。**
  * PNG在选择色板大小之余不使用任何有损压缩算法。因此她会生成最高质量的图像，不过和其他格式相比，其体积之大显而易见。谨慎使用。
  * 如果图像资源所包含的图像是由几何图形组成的，考虑将其转换成矢量（SVG）格式！
  * 如果图像资源包含文字，别这么干再想想。图像中的文字不能选择、不能搜索、不能缩放。如果你需要一个定制化的表现（为了品牌推广或者其他原因），使用网络字体。
1. **你是否要优化一张照片、截图或者一个类似的图像资源？使用JPEG。**
  * JPEG使用一系列有损及无损的优化手段来减小图像资源的文件体积。尝试不同的JPEG质量水平来找到你资源的最佳质量和文件体积之间的平衡点。

最后，一旦你决定来你资源的最佳的图像格式，以及它的设置，尝试添加使用WebP和JPEG XP编码的副本。这两种格式都是新的，而且不幸的（暂时）并未被所有浏览器支持，不过它们仍然可以为新客户端提供明显的节省——平均来说，WebP比同水平的JPEG[减少了30%的文件体积](https://developers.google.com/speed/webp/docs/webp_study)。

因为WebP和JPEG XP都还没有被普遍支持，你需要在你的应用或服务器上添加额外的逻辑来确保其提供合适的资源：

* 部分CDN提供图像优化服务，包括传递JPEG XR和WebP。
* 部分开源工具（比如用于Apache或者Nginx的PageSpeed）会自动进行优化，转换并提供合适的资源。
* 你可以添加其他的应用逻辑来探知客户端，检查它们支持哪些格式，并提供最合适的图像格式。

最后的最后，注意如果你在本地应用中使用web试图来呈现内容，那么你就拥有客户端的完全控制权，并且可以使用WebP独占！Facebook、Google+以及很多其他人在他们的应用中使用WebP来传递所有图像——这份节约绝对值得你这么做。想了解更多有关WebP的内容，可以查看Google I/O 2013上的演讲[WebP：配置更快、更小、更美的图像](https://www.youtube.com/watch?v=pS8udLMOOaE)。


## 工具和参数调整

没有一个可以应用于所有图像的完美格式、工具或者系列优化设置。想要获得最佳效果，你就必须根据图像内容、视觉及其他技术要求选择格式和设置。

<table class="table-2">
<colgroup><col span="1"><col span="1"></colgroup>
<thead>
  <tr>
    <th>工具</th>
    <th>描述</th>
  </tr>
</thead>
<tbody>
<tr>
  <td data-th="tool"><a href="http://www.lcdf.org/gifsicle/">gifsicle</a></td>
  <td data-th="description">创建和优化GIF图像</td>
</tr>
<tr>
  <td data-th="tool"><a href="http://jpegclub.org/jpegtran/">jpegtran</a></td>
  <td data-th="description">优化JPEG图像</td>
</tr>
<tr>
  <td data-th="tool"><a href="http://optipng.sourceforge.net/">optipng</a></td>
  <td data-th="description">无损PNG优化</td>
</tr>
<tr>
  <td data-th="tool"><a href="http://pngquant.org/">pngquant</a></td>
  <td data-th="description">有损PNG优化</td>
</tr>
</tbody>
</table>


不要惧怕尝试每个压缩工具的参数。调低质量，检查它的样子，然后换个姿势再来一次。当你找到一个不错的设置的时候，你可以把它应用在你网站上相似的图像上，但是不要假设所有的图像都必须要用相同的设置来压缩。。


## 提供不同尺寸的图像资源

{% include modules/takeaway.liquid list=page.key-takeaways.scaled-images %}

图像优化可以归结为两个条件：优化用于编码每个图像像素所需的比特数，和优化像素总数：图像的文件大小单纯就是像素总数乘以编码每个像素所需的比特数，无他。

因此，最简单且有效的图像优化技术之一，便是确保我们所要传送的资源的像素总数，不会比它将在浏览器中所展示的更多。听起来很简单，对吧？不幸的是，大多数页面的大量图像资源都失败了：通常他们会传送更大的资源，然后依赖浏览器去缩放它们——这也需要消耗额外的CPU资源——最终以较低分辨率显示。

<img src="images/resized-image.png" class="center" alt="Resized image">

{% include modules/remember.liquid title="Note" list=page.notes.resized %}

传送额外的像素，只是让浏览器帮我们缩小图像，这便错过了一个重大的减少并优化页面渲染中所需字节总数的机会。此外，要注意调整大小不仅是单纯的减少像素总数，也减小了其原始尺寸。

<table class="table-3">
<colgroup><col span="1"><col span="1"><col span="1"></colgroup>
<thead>
  <tr>
    <th>原始尺寸</th>
    <th>显示尺寸</th>
    <th>冗余像素</th>
  </tr>
</thead>
<tbody>
<tr>
  <td data-th="natural">110 x 110</td>
  <td data-th="display">100 x 100</td>
  <td data-th="overhead">110 x 110 - 100 x 100 = 2100</td>
</tr>
<tr>
  <td data-th="natural">410 x 410</td>
  <td data-th="display">400 x 400</td>
  <td data-th="overhead">410 x 410 - 400 x 400 = 8100</td>
</tr>
<tr>
  <td data-th="natural">810 x 810</td>
  <td data-th="display">800 x 800</td>
  <td data-th="overhead">810 x 810 - 800 x 800 = 16100</td>
</tr>
</tbody>
</table>

注意上面所列3种情况，显示尺寸均只比实际尺寸“小10像素而已”。然而我们要编码并传输的像素却明显大于原始尺寸！因此，你虽然可能无法保证每个资源都按其实际显示大小传输，**但你应该保证无用的像素数是最少的，而你的大尺寸的资源应该尽可能接近它的实际显示大小。**

## 图像优化清单

图像优化既是一门艺术也是一门科学：说艺术是因为对于如何最佳压缩特定图像，并没有一个确定的答案，而说其科学是因为现在已经有了很多成熟的技术和算法来显著减少图像体积。

在你优化你的图像时，这些提示应牢记在心：

* **优先矢量格式：** 矢量图是与分辨率无关而且可以自由缩放的，这使得它们非常适用于多设备及高分辨率世界。
* **最小化并压缩SVG资源：** 由大部分绘图应用生成的XML标记通常包含可去除的无用元数据，确保你的服务器设置能够对SVG资源使用GZIP压缩技术。
* **选择最合适的位图格式：** 确定你的功能需求，然后为每个资源选择最合适的格式。
* **为位图尝试最佳质量设置：** 不要担心调低“质量”设置，其结果通常不错，而且节约效果明显。
* **去除冗余的图像元数据：** 很多位图包含关于这个资源的无用元数据：地理信息、相机信息等等。用适当的工具去掉这些数据。
* **提供合适尺寸的图像：** 在服务器上缩放图像，以确保其“显示”尺寸尽可能接近其“原始”尺寸。要格外密切关注那些大图像，因为它们在缩放时占用了最大的系统开销！
* **自动化、自动化、自动化：** 使用自动化工具和基础架构，以长期确保你的所有图像资源均已被优化。


{% include modules/nextarticle.liquid %}

{% endwrap %}
