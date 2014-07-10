---
layout: article
title: "回应触控的状态性元素"
description: "
要确保用户能感受到自己的触控没被忽视，最简单的方式就是在他们进行点击时改变的你网站的UI用户界面。改变背景颜色就能够让一切变得不同，并且这也很容易做到。"
introduction: "触控屏幕在越来越多的设备上出现，从手机到桌面屏幕。当你的用户选择与你设计的用户界面相交互，你的应用程序需要以一种直观并且美观的方式回应他们的触摸。"
article:
  written_on: 2014-01-01
  updated_on: 2014-01-06
  order: 1
rel:
  gplusauthor: https://plus.google.com/+MattGaunt
key-takeaways:
  add-states:
    - 若要使你的网站让人感觉轻快和反应迅速，那么就为下面这些状态改变用户界面吧： :hover, :active 和 :focus。
    - 除非你要套用自己改造的用户界面，否则请不要改变一个浏览器对触摸和聚焦的默认反应。
    - 在那些用户会去触控的元素上，文本信息应禁用被选取的功能，除非你有合理的原因可能需要用户选取或者拷贝这些文字信息。    
remember:
  disable-user-select:
    - 如果元素上的信息对用户来说有帮助（电话号码，邮件，地址等等），那么你应该注意不能无效化用户选择。
  override-default:
    - 如果你要执行自己的浏览方式，你只有选择覆盖原来的浏览方式！
collection: touch-input
---

{% wrap content%}

## 添加触控状态

你曾经有过触摸或点击一个网页的元素，却不确定网站是否真正侦测到了你的触摸或者点击的经历吗？

当用户触摸你用户界面的一部分的时候，简单地替换一下元素颜色，这会给予用户一种网页正常运行的确示。这样不仅会缓解用户失望的情绪，并且能够为你的网站赋予一种轻快和热情的感觉。

### 为每次的点击状态使用伪类来改变用户界面

支持触摸的最快的方式是改变用户界面以应对状态下一个DOM元素的变化。

{% include modules/takeaway.liquid list=page.key-takeaways.add-states %}

DOM元素可能存在于以下状态中 default, focus, hover, 和 active.要为每一个状态改变用户界面，我们需要添加样式到以下伪类： `:hover`，` :focus`和`:active`，即如下所示：


{% include_code ../_code/states-example.html btnstates css %}

See [Pseudo classes for touch states](#pseudo-classes-for-touch-states):

![Image illustrating the different colors for button states](images/button-states.png)

### 悬停和聚焦

在大多数的移动端浏览器上，当一个元素被点击后*悬停*与／或*聚焦*属性会被应用于其上。

仔细的推敲你要设置什么样式以及用户完成触控之后，他们会呈现给用户什么样的外观。

要谨记锚点标签和按钮可能在不同的浏览器中的响应行为是不一样的，因此我们假设在某些情况下*悬停* will remain and in others *focus* will remain.

### 在iOS中启用激活状态支持

不幸的是，Safar在iOS上不能默认应用*active*状态，要想启用这个状态，你需要在*文档主体*或者每一个元素当中添加一个`touchstart`事件监听器。

你应在这么做之前使用用户的浏览器判别测试，从而让前述流程只在iOS设备上运行。

在主体当中添加一个 touchstart 比将它应用于所有DOM元素这种方式要更有优势，但是这样可能会在滚动页面时造成表现性能上的一些问题。

{% highlight js %}
window.onload = function() {
  if(/iP(hone|ad)/.test(window.navigator.userAgent)) {
    document.body.addEventListener('touchstart', function() {}, false);
  }
};
{% endhighlight %}

另一种方法是将 touchstart 监听器添加到页面上所有互动性元素中，缓解一些性能上的压力。 

{% highlight js %}
window.onload = function() {
  if(/iP(hone|ad)/.test(window.navigator.userAgent)) {
    var elements = document.querySelectorAll('button');
    var emptyFunction = function() {};
    for(var i = 0; i < elements.length; i++) {
      elements[i].addEventListener('touchstart', emptyFunction, false);
    }
  }
};
{% endhighlight %}

### 为触摸状态覆盖默认的浏览方式

当你为不同的状态添加样式时，你会注意到大多数的浏览器会对用户的触控反应实施他们自己设定的样式，当你想要加入自己样式时你应该覆盖改写掉这些默认设置。

{% include modules/remember.liquid title="Remember" list=page.remember.override-default %}

#### 覆盖点击高亮样式

当移动设备初次发布的时候，许多的网站还没有为激活状态进行适配。因此，许多浏览器为元素添加高亮颜色和样式应对用户的触摸。

Safari和Chrome浏览器添加了一个高亮点击色，而且能够通过`-webkit-tap-highlight-color` CSS属性禁止高亮点击色：

{% include_code ../_code/states-example.html webkit-specific css %}

Windows Phone设备上的Internet Explorer拥有相似的行为，但是其是通过对大尺寸的标签的点击来实现的：

{% highlight html %}
<meta name="msapplication-tap-highlight" content="no">
{% endhighlight %}

#### 覆盖FirefoxOS的按键状态方式

Firefox的`-moz-focus-inner`伪类集包括了一个可触摸元素的outline。你可以通过设置`border: 0`来移除outline。

If you are
如果你正在使用一个`<button>`元素，你会得到一个应用于你的按键的gradient，你可以通过设置`background-image: none`移除这个gradient。
{% include_code ../_code/states-example.html ff-specific css %}

#### 覆盖聚焦状态下元素的Outline

在使用`outline: 0`让一个元素被聚焦的时候，淡化其他缩略图颜色。
{% highlight css %}
.btn:focus {
  outline: 0;

  // Add replacement focus styling here (i.e. border)
}
{% endhighlight %}

### 使在用户界面上回应触摸的用户选择无效化

如果用户在触摸屏上进行长按操作，一些浏览器将会选择文本。在用户偶然过久地按着一个按键的情况下，这会造成不良的用户体验。通过使用`user-select` CSS属性，你可以防止其发生。

{% highlight css %}
-moz-user-select: none;
-webkit-user-select: none;
-ms-user-select: none;
user-select: none;
{% endhighlight %}

{% include modules/remember.liquid title="Remember" list=page.remember.disable-user-select %}

## 参考

### 用于触摸状态的伪类

<table class="table-3">
  <thead>
    <tr>
      <th>Class</th>
      <th>Example</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Class">:hover</td>
      <td data-th="Example"><img alt="Button in Pressed State" src="images/btn-hover-state.png"></td>
      <td data-th="Description">
        当光标悬停在一个元素上方时就会进入如此状态。用户界面中悬停状态产生的外观改变对鼓励用户和元素交互来说是非常有帮助的。
      </td>
    </tr>
    <tr>
      <td data-th="Class">:focus</td>
      <td data-th="Example">
        <img alt="Button with Focus State" src="images/btn-focus-state.png">
      </td>
      <td data-th="Description">
当你用tab切换遍一个页面上的元素时，这意味着你把元素的聚焦点在彼此之间切换。聚焦状态会让用户明白正在与之交互的元素。同时可以让用户简单地使用键盘操控你的用户界面。
      </td>
    </tr>
    <tr>
      <td data-th="Class">:active</td>
      <td data-th="Example">
        <img alt="Button in Pressed State" src="images/btn-pressed-state.png">
      </td>
      <td data-th="Description">
        这是一个元素被选择时的状态，例如当用户点击或者触摸一个元素时，元素就会如此显示。
      </td>
    </tr>
  </tbody>
</table>

{% include modules/nextarticle.liquid %}

{% endwrap %}
