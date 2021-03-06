---
layout: article
title: "选择最佳输入方案"
description: "每一次点击都包含在内，用户会感谢那些网站：在他们输入电话号码的时候自动呈现拨号键盘，或者是在他们输入信息前提前填充完成表单。所以，在你的表格中，寻找能够去除多余点击的机会吧。"
introduction: "每一次点击都包含在内。用户会感谢那些网站：在他们输入电话号码的时候自动呈现拨号键盘，或者是在他们输入信息前提前填充完成表单。所以，在你的表格中，寻找能够去除多余点击的机会吧。"
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 1
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
collection: form-input
key-takeaways:
  choose-best-input-type:
    - 为你的数据选择最适合的输入方案以简化输入流程。
    - 当用户在 <code>datalist</code> 元素下输入时，为用户提供建议.
remember:
  use-placeholders:
    - 当焦点集中在一个元素上时，占位符就会消失。因此他们不能替代标签。
      占位符应该作为一种帮助，在用户所需的格式和内容上进行导航。
  recommend-input:
    - 自动完成只会在当表格出现的情况下运行。
  use-datalist:
    - <code>datalist</code> 值作为建议提供给用户，但是用户不会局限于所提供的建议中。
  provide-real-time-validation:
    - 即使存在客户端一方的输入认证，在服务器上认证数据以确保你的数据的统一性和安全性同样重要。
  show-all-errors:
    - 你应该一次性告诉用户表格存在的所有问题，而不是分时段告诉用户。
  request-auto-complete-flow:
    - 如果你正在搜寻任何私人信息或信用卡数据，那么请确保这个页面在SSL下运行。
      否则对话框会警告用户他们的信息可能不能得到安全保障。
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

{% include modules/takeaway.liquid list=page.key-takeaways.choose-best-input-type %}

### HTML5 input types

HTML5 介绍了一系列新的输入方案。这些新方案提示浏览器应该为屏幕键盘显示怎样的键盘布局。用户能够更加容易输入所需信息，而不一定要改变他们的键盘布局，而且，用户只需要注意输入类型下合适的按键。

<table class="table-2 inputtypes">
  <thead>
    <tr>
      <th data-th="Input type">Input <code>type</code></th>
      <th data-th="Typical keyboard">Typical Keyboard</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Input type">
        <code>url</code><br>若要输入一个网址，则必须以有效的网址组合开始，例如： <code>http://</code>, <code>ftp://</code> or <code>mailto:</code>.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/url-ios.png" srcset="imgs/url-ios.png 1x, imgs/url-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>tel</code><br>若要输入电话号码，则要采用一个特殊的句法 <b>not</b>来认证。所以如果你想保证一个特殊的格式可行，你可以使用模版。
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/tel-android.png" srcset="imgs/tel-android.png 1x, imgs/tel-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>email</code><br>若要输入邮件地址，@符号应该默认出现在键盘上。如果要提供不止一个邮件地址，你可以添加多属性实现。
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/email-android.png" srcset="imgs/email-android.png 1x, imgs/email-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>search</code><br>文本输入字段的风格和平台的搜索字段的风格是统一的。
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/plain-ios.png" srcset="imgs/plain-ios.png 1x, imgs/plain-ios-2x.png 2x" class="keybimg">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>number</code><br>若要进行数字的输入，这些数字能够是任何合理的整型值或是浮点型值。
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/number-android.png" srcset="imgs/number-android.png 1x, imgs/number-android-2x.png 2x" class="keybimg">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>range</code><br>若要输入号码，但是却和号码输入类型不同，那么值并不重要。这些值会以滑块控件的形式显示在用户面前。
</td>
      <td data-th="Typical keyboard">
        <img src="imgs/range-ios.png">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>datetime-local</code><br>要在时区为本地时区的地方输入一个日期值和时间值。
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/datetime-local-ios.png" srcset="imgs/datetime-local-ios.png 1x, imgs/datetime-local-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>date</code><br>仅要输入一个日期值，而且没有提供时区。
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/date-android.png" srcset="imgs/date-android.png 1x, imgs/date-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>time</code><br>仅要输入一个时间值，而且没有提供时区。
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/time-ios.png" srcset="imgs/time-ios.png 1x, imgs/time-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>week</code><br>仅要输入一个星期值，而且没有提供时区。      
</td>
      <td data-th="Typical keyboard">
        <img src="imgs/week-android.png" srcset="imgs/week-android.png 1x, imgs/week-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>month</code><br>仅要输入一个月份值，而且没有提供时区。
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/month-ios.png" srcset="imgs/month-ios.png 1x, imgs/month-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>color</code><br>要选择一个颜色。
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/color-android.png" srcset="imgs/color-android.png 1x, imgs/color-android-2x.png 2x">
      </td>
    </tr>
  </tbody>
</table>

### 在输入时用datalist提供建议

`datalist`元素并不是一种输入类型，它是一个建议输入值的列表，并和格式字段相关。在用户输入的时候，它让浏览器给用户推荐自动完成的选项。不像选择元素，用户必须浏览冗长的列表来搜寻他们所寻找的值，并且限制用户停留在列表上。`datalist`在用户输入时会提供提示。

{% include_code _code/order.html datalist %}

{% include modules/remember.liquid title="Remember" list=page.remember.use-datalist %}

{% include modules/nextarticle.liquid %}

{% endwrap %}
