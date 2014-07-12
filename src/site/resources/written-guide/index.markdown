---
layout: default
title: "书写风格指导"
description: "书写风格指导"
class: "page--styleguide"
article:
  written_on: 2014-01-01
  updated_on: 2014-01-06
  order: 3
collection: resources
---

{% wrap content %}

{% include modules/breadcrumbs.liquid %}

# {{ page.title }}

{% include modules/toc.liquid %}


## IA

所有从主菜单链接到的都是“着陆页”。着陆页是一些章节的集合。章节是一些指导。指导是某一特定部分的内容。

着陆页会链接到一个章节的详细页面，也会有在该章节下的指导列表。

章节会有个主页，其中包括内含指导的高度概括和指导列表。也会在标题部分包含一个视频介绍。

## 大写和命名
  * 在本站内需要使用连字符的词，没有连字符时需要首字母大写（比如"Multi-Device"和"Peer-to-Peer"）

### 站点章节标题
  * 标题首字母大写（比如应是"Multi-Device Layouts"而非"Multi-device layouts"）
  * 避免在顶级章节标题中使用动词。

### 文章标题
  * 标题首字母大写（比如应是"Responsive Web Design Basics"而非"Responsive web design basics"）。
  * 可能的话使用祈使动词（比如应是"Set the viewport"而非"Setting the viewport"）。

### 文章内的小标题
  * 文章内的小标题句首字母大写："Use placeholders for images"。
  * 可能的话使用祈使动词（比如应是"Set the viewport"而非"Setting the viewport"）。

## 链接到另外一篇文章
  * 将我们的文章作为相关阅读：加它们进来。
  * 不要吝惜外部资源，需要时将其引入（比如链接到API参考，不过不要链接到其他开发者的解释）。

## "移动设备" vs. "多设备" vs "多屏幕" vs "移动唯一" vs "移动先行"
  * 为一致性使用"multi-device"，除非情况确实需要如此精度。

## 文章长度
  * 每个文章只有一个“核心”（比如“在你的表单中使用正确的input type”）。

## 口吻
  * 主动的，而非被动的。
  * 使用现在时，除非牵涉到将来的事件（比如修复将来的问题）。
  * 非正式代词和缩写可以简化文本，但不要过度使用。
  * 避免不必要的形容词。

## 代码样例
  * 每篇文章需要至少有一个必要的使用需求的例子。

## 重点/太长；懒得读
  * 每篇文章都要有太长；懒得读部分。
  * 使用“太长；懒得读”而非“重点”。
  * 确保每一条都简短。

## 媒体
  * 所有图像的长宽比需为3:5或5:3。
  * 图像在部署时会被压缩。你不用担心需要自行压缩图像。

{% endwrap %}
