---
layout: article
title: "选择最佳的输入类型"
description: "每一次敲击都包括在内。用户会对此表示感谢，即在他们需要输入数字号码的时候能够自动显示数字键盘，或者用户需要输入时能够自动将表单提前。在你的表单中，寻找一切机会以排除多余的敲击。"
introduction: "每一次敲击都包括在内。用户会对此表示感谢，即在他们需要输入数字号码的时候能够自动显示数字键盘，或者用户需要输入时能够自动将表单提前。在你的表单中，寻找一切机会以排除多余的敲击。"
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 1
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
collection: form-input
key-takeaways:
  choose-best-input-type:
    - 选择匹配你数据的最佳输入类型以简化输入过程。
    - 在用户以<code>datalist</code>元素输入的时候给予提示。
remember:
  use-placeholders:
    - 当焦点被一个元素占用时，占位符会自动隐藏。因此，占位符不能替代标签。他们应该被用来作为所需格式和所需内容上的一种援助，以帮助并为用户提供导航。
  recommend-input:
    - Auto-complete only works when the form method is post.
  use-datalist:
    - <code>datalist</code> 的价值在于提供建议，同时，用户不会被这些所提供的建议所限制。
  provide-real-time-validation:
    - 即使有使用端的认证，但是认证服务器上的数据以确保你数据的统一性和安全性是非常重要的。
  show-all-errors:
    - 你应该向用户一次性展示表单的所有问题，而不是阶段性地展示。
  request-auto-complete-flow:
    - 如果你请求任何种类的私人星系或者信用卡数据，请确保网页处于SSL服务状态。否则，将会弹出对话框警告用户他们的信息可能会不安全。
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

### HTML5输入类型

HTML5 introduced了许多新的输入类型。这些新的输入类型可以提示浏览器在屏幕上应显示何种键盘布局类型。这样用户就能够更容易的输入网站所需要的信息，而不是一定要切换键盘。用户只会看到在那种输入类型下合适的按键布局。

<table class="table-2 inputtypes">
  <thead>
    <tr>
      <th data-th="Input type">输入类型 Input <code>type</code></th>
      <th data-th="Typical keyboard">典型键盘</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Input type">
        <code>url</code><br> 输入一个URL时，必须以一个有效的URL格式来开头，例如(For entering a URL. It must start with a valid URI scheme,
        for example) <code>http://</code>, <code>ftp://</code> or <code>mailto:</code>.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/url-ios.png" srcset="imgs/url-ios.png 1x, imgs/url-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>tel</code><br>For entering phone numbers. It does <b>not</b>
        enforce a particular syntax for validation, so if you want to ensure
        a particular format, you can use pattern.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/tel-android.png" srcset="imgs/tel-android.png 1x, imgs/tel-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>email</code><br>For entering email addresses, and hints that
        the @ should be shown on the keyboard by default. You can add the
        multiple attribute if more than one email address will be provided.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/email-android.png" srcset="imgs/email-android.png 1x, imgs/email-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>search</code><br>A text input field styled in a way that is
        consistent with the platform's search field.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/plain-ios.png" srcset="imgs/plain-ios.png 1x, imgs/plain-ios-2x.png 2x" class="keybimg">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>number</code><br>For numeric input, can be any rational
        integer or float value.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/number-android.png" srcset="imgs/number-android.png 1x, imgs/number-android-2x.png 2x" class="keybimg">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>range</code><br>For number input, but unlike the number input
        type, the value is less important. It is displayed to the user as a
        slider control.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/range-ios.png">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>datetime-local</code><br>For entering a date and time value
        where the time zone provided is the local time zone.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/datetime-local-ios.png" srcset="imgs/datetime-local-ios.png 1x, imgs/datetime-local-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>date</code><br>For entering a date (only) with no time zone
        provided.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/date-android.png" srcset="imgs/date-android.png 1x, imgs/date-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>time</code><br>For entering a time (only) with no time zone
        provided.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/time-ios.png" srcset="imgs/time-ios.png 1x, imgs/time-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>week</code><br>For entering a week (only) with no time zone
        provided.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/week-android.png" srcset="imgs/week-android.png 1x, imgs/week-android-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>month</code><br>For entering a month (only) with no time zone
        provided.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/month-ios.png" srcset="imgs/month-ios.png 1x, imgs/month-ios-2x.png 2x">
      </td>
    </tr>
    <tr>
      <td data-th="Input type">
        <code>color</code><br>For picking a color.
      </td>
      <td data-th="Typical keyboard">
        <img src="imgs/color-android.png" srcset="imgs/color-android.png 1x, imgs/color-android-2x.png 2x">
      </td>
    </tr>
  </tbody>
</table>

### 在用户以datalist元素输入的时候给予提示

`datalist`元素并不是一种输入类型。但是一系列的建议输入和表单标签相关联才会起作用。当用户输入时，datalist元素会让浏览器弹出自动输入的提示。不像选择元素，用户必须扫视长篇以找到他们所需要的重要信息，同时又限制用户停留在列表中。当他们在输入的时候，`datalist`给予用户提示。
{% include_code _code/order.html datalist %}

{% include modules/remember.liquid title="Remember" list=page.remember.use-datalist %}

{% include modules/nextarticle.liquid %}

{% endwrap %}
