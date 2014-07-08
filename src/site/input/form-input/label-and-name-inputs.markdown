---
layout: article
title: "合适的标签和名称输入"
description: "表单很难在移动设备上完全表现出来。体验最佳的表单是那些仅需少量输入的表单。"
introduction: "表单很难在移动设备上完全表现出来。体验最佳的表单是那些仅需少量输入的表单。好的表单能够提供给用户恰逢时宜的输入类型。键盘应该改变类型以匹配用户的输入场景。当用户在日历中添加一个事件时，请使你的用户时刻保持被提醒的状态。认证工具则应该告诉用户在提交表格前需要做些什么。"
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 2
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
collection: form-input
key-takeaways:
  label-and-name:
    - 请在表单输入中使用<code>label</code>s ，同时保证他们在输入框在激活时是可见的。
    - 请使用 <code>placeholder</code>s 为用户提供你所期待的向导
    - 请帮助浏览器自动完成表单，使用已建立的<code>name</code>'s
      作为元素和包括<code>autocomplete</code> 属性。
remember:
  use-placeholders:
    - 当焦点被一个元素占用时，占位符会自动隐藏。因此，占位符不能替代标签。他们应该被用来作为所需格式和所需内容上的一种援助，以帮助并为用户提供导航。
  recommend-input:
    - Auto-complete only works when the form method is post.
  use-datalist:
    - The <code>datalist</code> values are provided as suggestions, and users
      are not restricted to the suggestions provided.
  provide-real-time-validation:
    - Even with client-side input validation, it is always important to
      validate data on the server to ensure consistency and security in your data.
  show-all-errors:
    - You should show the user all of the issues on the form at once, rather than showing them one at a time.
  request-auto-complete-flow:
    - If you're asking for any kind of personal information or credit card
      data, ensure the page is served via SSL.  Otherwise the dialog will
      warn the user their information may not be secure.
---
{% wrap content %}

<style>
  img, video, object {
    max-width: 100%;
  }

  img.center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  table.inputtypes th:nth-of-type(2) {
    min-width: 270px;
  }

  table.tc-heavyright th:first-of-type {
    width: 30%;
  }
</style>

{% include modules/takeaway.liquid list=page.key-takeaways.label-and-name %}

### 标签的重要性

`label` 元素为用户提供操作方向，告诉他们在一个表单元素中什么是他们所需要的信息。通过放置输入元素在`label`元素中，或者使用"`for`"属性，每一个`label`和就会和每一个输入元素相互关联。通过给表单元素添加标注同样也可以帮助扩大触摸目标的面积：即如果用户把焦点集中在输入元素上时，可以触摸标注或者是输入框的方式来实现。 
{% include_code _code/order.html labels %}

### label尺寸与位置

labels与输入元素应该有足够的尺寸以便容易点击。在描述视窗内，标签字符应当位于输入元素的上方。在全局视窗内，标签字符应当位于输入元素的两旁。请确保标签字符与其相应的输入框同时可见。请注意自定义滚动处理程序，它可能将输入元素移动至页面顶部而隐藏标签。或者是位于输入元素下方的labels会被虚拟键盘而遮盖。

### 使用占位符

占位符属性为用户提供输入内容提示，它通过高亮文本显示直到元素得到点击为止。

<input type="text" placeholder="MM-YYYY">

{% highlight html%}
<input type="text" placeholder="MM-YYYY" ...>
{% endhighlight %}


{% include modules/remember.liquid title="Remember" list=page.remember.use-placeholders %}

### 使用元数据使自动完成成为可能

当网站为用户节省时间，自动填入通用字符，例如：名字、邮件地址和其他常用的表字符时，用户会感到非常满足。添加元数据能够帮助减少潜在的输入错误 - 特别是在虚拟键盘和小型设备上。

浏览器会使用heuristics来决定哪个字符他们可以自动完成[auto-populate](https://support.google.com/chrome/answer/142893)[based on
previously specified data by the
user](https://support.google.com/chrome/answer/142893)，并且，通过在输入元素中提供名字属性和自动完成属性，你可以给予浏览器提示。 

举例来说，为了提示浏览器它应该自动完成表单，包括用户姓名，邮件地址和手机号码，你应该使用:

{% include_code _code/order.html autocomplete %}


### Recommended input `name` and `autocomplete` attribute values

<table class="table-3 autocompletes">
  <thead>
    <tr>
      <th data-th="Content type">Content type</th>
      <th data-th="name attribute"><code>name</code> attribute</th>
      <th data-th="autocomplete attribute"><code>autocomplete</code> attribute</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Content type">Name</td>
      <td data-th="name attribute">
        <code>name</code>
        <code>fname</code>
        <code>mname</code>
        <code>lname</code>
      </td>
      <td data-th="autocomplete attribute"><code>name</code></td>
    </tr>
    <tr>
      <td data-th="Content type">Email</td>
      <td data-th="name attribute"><code>email</code></td>
      <td data-th="autocomplete attribute"><code>email</code></td>
    </tr>
    <tr>
      <td data-th="Content type">Address</td>
      <td data-th="name attribute">
        <code>address</code>
        <code>city</code>
        <code>region</code>
        <code>province</code>
        <code>state</code>
        <code>zip</code>
        <code>zip2</code>
        <code>postal</code>
        <code>country</code>
      </td>
      <td data-th="autocomplete attribute">
        <code>street-address</code>
        <code>locality</code>
        <code>region</code>
        <code>postal-code</code>
        <code>country</code>
      </td>
    </tr>
    <tr>
      <td data-th="Content type">Phone</td>
      <td data-th="name attribute">
        <code>phone</code>
        <code>mobile</code>
        <code>country-code</code>
        <code>area-code</code>
        <code>exchange</code>
        <code>suffix</code>
        <code>ext</code>
      </td>
      <td data-th="autocomplete attribute"><code>tel</code></td>
    </tr>
    <tr>
      <td data-th="Content type">Credit Card</td>
      <td data-th="name attribute">
        <code>ccname</code>
        <code>cardnumber</code>
        <code>cvc</code>
        <code>ccmonth</code>
        <code>ccyear</code>
        <code>exp-date</code>
        <code>card-type</code>
      </td>
      <td data-th="autocomplete attribute">
        <code>cc-name</code>
        <code>cc-number</code>
        <code>cc-csc</code>
        <code>cc-exp-month</code>
        <code>cc-exp-year</code>
        <code>cc-exp</code>
        <code>cc-type</code>
      </td>
    </tr>
  </tbody>
</table>

The `autocomplete` attributes should be prefixed with either `shipping` or `billing`, depending on the context.

{% include modules/remember.liquid title="Remember" list=page.remember.recommend-input %}

### `autofocus`自动聚焦属性

在一些表单中，例如在Google主页，你唯一想让用户做的事情是填写特定的字符，因此你可以添加`autofocus`属性。当添加自动聚焦属性后，桌面浏览器会立即将聚焦于输入表单，目的是为了让用户更容易开始使用这个表单。移动浏览器则忽略了`autofocus`属性，这是为了防止键盘随机不定的出现的情况 to prevent the keyboard from randomly
appearing。

在使用自动聚焦属性时请注意，因为它可能取得键盘焦点，并潜在地禁用了用作导航的退格符
and potentially preventing the backspace character from being used for
navigation。

{% highlight html %}
<input type="text" autofocus ...>
{% endhighlight %}

{% include modules/nextarticle.liquid %}

{% endwrap %}
