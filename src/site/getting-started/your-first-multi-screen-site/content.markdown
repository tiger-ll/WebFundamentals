---
layout: article
title: "创造你自己的结构与内容"
description: "对任何网站来讲, 网站的内容一直都是最重要的因素之一. 在这个指南当中, 我们会教你如何快速的打造你的第一个多画面结构网站."
introduction: "对任何网站来讲, 网站的内容一直都是最重要的因素。因此，我们应该为了内容而设计而不是由设计决定内容。在这个指南中，我们先确定我们需要的内容，在此内容的基础上创建一个页面结构，然后在简单的能够适应任何宽度的线性布局中进行展示。"
notes:
  styling:
    - Styling will come later
article:
  written_on: 2014-04-17
  updated_on: 2014-04-23
  order: 1
collection: multi-screen
related-guides:
  create-amazing-forms:
    -
      title: Create amazing forms
      href: input/form-input/
      section:
        id: user-input
        title: "Forms"
        href: input/form-input/
    -
      title: Label and name inputs correctly
      href: input/form-input/label-and-name-inputs.html
      section:
        id: user-input
        title: "Forms"
        href: input/form-input/
    -
      title: Choose the best input type
      href: input/form-input/choose-the-best-input-type.html
      section:
        id: user-input
        title: Forms
        href: input/form-input/
  video:
    -
      title: Using video effectively
      href: media/video/
      section:
        id: introduction-to-media
        title: "Video"
        href: media/
    -
      title: Change the starting position
      href: media/video/
      section:
        id: introduction-to-media
        title: "Video"
        href: media/
    -
      title: Include a poster image
      href: media/video/
      section:
        id: introduction-to-media
        title: "Video"
        href: media/
  images:
    -
      title: Using images effectively
      href: media/images/
      section:
        id: introduction-to-media
        title: "Images"
        href: media/
    -
      title:  Correct use of images in markup
      href: media/images/#images-in-markup
      section:
        id: introduction-to-media
        title: "Images"
        href: media/
    -
      title: Image optimization
      href: performance/optimizing-content-efficiency/image-optimization.html
      section:
        id: introduction-to-media
        title: "Images"
        href: media/

key-takeaways:
  content-critical:
    - 首先确定你需要的内容。
    - 为宽和窄的视区勾画出信息架构 (Information Architecture,IA)。
    - 使用内容创建页面的框架，但不添加样式。
---

{% wrap content %}

{% include modules/toc.liquid %}

## 创建页面结构

我们需要展示:

1.  一个文本域，能够在高层次描述我们的产品 “CS256: 移动web开发” 教程
2.  一个表单，收集对我们产品有兴趣的用户的信息
3.  一个深度的介绍和视频
4.  使用中的产品的图像
5.  一个数据表格，用来支持描述的信息

{% include modules/takeaway.liquid list=page.key-takeaways.content-critical %}

我们也为宽和窄的视区画了粗略的信息架构和布局。

<div class="demo clear" style="background-color: white;">
  <img class="g-wide--1 g-medium--half" src="images/narrowviewport.png" alt="Narrow Viewport IA">
  <img  class="g-wide--2 g-wide--last g-medium--half g--last" src="images/wideviewport.png" alt="Wide Viewport IA">
</div>

这样可以很容易的转换为在下面的项目中使用的粗略的框架页面。

{% include_code _code/addstructure.html structure %}

## 向页面添加内容

网站的基本结构已经完成。我们知道我们需要的部分，在这些部分中要展示的内容，以及在整个信息架构中的位置。我们现在可以开始构建出这个网站了。

{% include modules/remember.liquid title="注意" inline="true" list=page.notes.styling %}

### 创建标题和表单

标题和请求通知的表单是我们页面的关键组件。这些必须要立即展示给用户。  

在标题中，添加一些简单的内容去介绍课程。

{% include_code _code/addheadline.html headline %}

我们还需要完成这个表单。它是一个简单的表单，来收集用户名，电话号码和一个适合给他们打电话的时间。

所有表单都应该有标签(label)和占位文字(placeholder)，方便用户能快速锁定焦点，明白他们应该如何填写，以及帮助辅助工具理解表单的结构。

我们将添加语义类型，使其能在移动设备上快速简单的让用户输入内容。例如，当输入一个电话号码时，用户只应该看到一个拨号键盘。

{% include_code _code/addform.html form %}

{% include modules/related_guides.liquid inline=true list=page.related-guides.create-amazing-forms %}

### 创建视频和信息部分

内容中的视频和信息部分会包含更深入的信息。它会包括一个我们产品特性的项目符号列表，也会包含一个视频的占位符，其中展示我们的产品正在为用户工作。

{% include_code _code/addcontent.html section1 %}

视频通常用一种更加互动的方式来描述内容，通常用来展示一个产品或概念。

通过遵循最佳实践，你可以很容易的在你的网站上集成视频。

*  添加 `controls` 属性让人更方便的播放视频。
*  添加 `poster` 图像给用户视频内容的预览。
*  基于支持的视频格式，添加多个 `<source>` 元素.
*  添加备用文字让人下载，如果他们不能在窗口内播放。

{% include_code _code/addvideo.html video html %}

{% include modules/related_guides.liquid inline=true list=page.related-guides.video %}

### 创建图像部分

没有图像的网站会显得有点无聊。网站上有两种类型的图像：

*  内容图像 &mdash; 内联在文档中的图像，用来传递关于内容的额外信息。
*  样式图像 &mdash; 用来让网站看起来更好看的图像；通常是背景图像，图案和渐变。我们将会在[下一篇文章]({{site.baseurl}}{{page.article.next.url}})中介绍.

图像部分是我们会在产品中用到的内容图像的集合。

内容图像对传递网页的含义是至关重要的。联想一下报纸文章中使用的图像。
我们所用的图片是这个项目的导师们，Chris Wilson, Peter Lubbers 和 Sean Bannet。
{% include_code _code/addimages.html images html %}

图像缩放设置为屏幕宽度的100%。这会在移动设备上工作良好，但在桌面上则没那么好。我们将在响应式设计部分解决这个问题。

{% include modules/related_guides.liquid inline=true list=page.related-guides.images %}

### 添加表格化数据部分

最后的部分是一个简单的表格，用来显示关于产品的具体产品统计。

表格应只用来展示表格数据，如信息模型。

{% include_code _code/addcontent.html section3 %}

### 添加一个Footer

大多数网站需要一个footer来展示某些内容，比如免责声明，使用条款，以及其他的一些不应该放在主导航栏的内容。

在我们的网站上，我们只链接了使用条款，联系页面，以及一个社交媒体简介页面。

{% include_code _code/addcontent.html footer %}

## 总结

我们已经创建了网站的大纲，我们已经确定了所有的主要结构元素。我们也确保我们准备好了所有相关的内容来满足我们的业务需求。

<div class="clear">
  <img class="g-wide--2 g-medium--half" src="images/content.png" alt="Content" style="max-width: 100%;">
  <img  class="g-wide--2 g-wide--last g-medium--half g--last" src="images/narrowsite.png" alt="" style="max-width: 100%;">
</div>

你会注意到现在的页面看起来很糟糕；这是故意的。内容是任何网站中最重要的方面，我们需要确保我们有一个良好坚实的信息架构和密度。本指南已经给我们了一个很好的构建基础。我们将会在下个指南中添加内容的样式。

{% include modules/nextarticle.liquid %}

{% endwrap %}
