---
layout: article
title: "提供实时认证"
description: "实时数据认证不仅保证你的数据条目清晰，它同时也帮助提高用户体验。目前主流浏览器都拥有一些内置工具以帮助提供实时认证，并且可以防止用户提交无效信息。视觉提示应该被用来提示一个表单是否准确地被填写。"
introduction: "实时数据认证不仅保证你的数据条目清晰，它同时也帮助提高用户体验。目前主流浏览器都拥有一些内置工具以帮助提供实时认证，并且可以防止用户提交无效信息。视觉提示应该被用来提示一个表单是否准确地被填写。"
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 3
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
collection: form-input
key-takeaways:
  provide-real-time-validation:
    - 利用浏览器内置的实时认证属性，比如：
      <code>pattern</code>, <code>required</code>, <code>min</code>,
      <code>max</code>, 等等。
    - 使用JavaScript并且限制认证API满足更复杂的认证需求。
    - 实时显示认证错误，并且如果用户试图提交无效表单，那么就显示出用户需要修改的标签。
remember:
  use-placeholders:
    - Placeholders disappear as soon as focus is placed in an element, thus
      they are not a replacement for labels.  They should be used as an aid
      to help guide users on the required format and content.
  recommend-input:
    - Auto-complete only works when the form method is post.
  use-datalist:
    - The <code>datalist</code> values are provided as suggestions, and users
      are not restricted to the suggestions provided.
  provide-real-time-validation:
    - 即使有使用端的认证，但是认证服务器上的数据以确保你数据的统一性和安全性是非常重要的。
  show-all-errors:
    - 你应该向用户一次性展示表单的所有问题，而不是阶段性地展示。
  request-auto-complete-flow:
    - If you're asking for any kind of personal information or credit card
      data, ensure the page is served via SSL.  Otherwise the dialog will
      warn the user their information may not be secure.
---
{% wrap content %}

<style>
  table.inputtypes th:nth-of-type(2) {
    min-width: 270px;
  }

  table.tc-heavyright th:first-of-type {
    width: 30%;
  }
</style>

{% include modules/takeaway.liquid list=page.key-takeaways.provide-real-time-validation %}

### 使用这些属性以认证输入

#### `pattern` 模版属性

`pattern` 模板属性详细阐述了用作认证输入表单的 [正则表达式（regular
expression）](http://en.wikipedia.org/wiki/Regular_expression) 。例如：验证一个美国邮编（5个数字，有时可能由1个破折号再加上4个额外的数字），我们会设置像这样的`pattern` :

{% highlight html %}
<input type="text" pattern="^\d{5,6}(?:[-\s]\d{4})?$" ...>
{% endhighlight %}

##### Common regular expression patterns

<table class="table-2 tc-heavyright">
  <thead>
    <tr>
      <th data-th="Description">描述</th>
      <th data-th="Regular expression">Regular expression</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Description">邮编</td>
      <td data-th="Regular expression"><code>[a-zA-Z\d\s\-\,\#\.\+]+</code></td>
    </tr>
    <tr>
      <td data-th="Description">Zip Code (美国邮编)</td>
      <td data-th="Regular expression"><code>^\d{5,6}(?:[-\s]\d{4})?$</code></td>
    </tr>
    <tr>
      <td data-th="Description">IP地址</td>
      <td data-th="Regular expression"><code>^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$</code></td>
    </tr>
    <tr>
      <td data-th="Description">信用卡号码</td>
      <td data-th="Regular expression"><code>^(?:4[0-9]{12}(?:[0-9]{3})?|5[1-5][0-9]{14}|3[47][0-9]{13}|3(?:0[0-5]|[68][0-9])[0-9]{11}|6(?:011|5[0-9]{2})[0-9]{12}|(?:2131|1800|35\d{3})\d{11})$</code></td>
    </tr>
    <tr>
      <td data-th="Description">社会安全保险号码</td>
      <td data-th="Regular expression"><code>^\d{3}-\d{2}-\d{4}$</code></td>
    </tr>
    <tr>
      <td data-th="Description">北美电话号码</td>
      <td data-th="Regular expression"><code>^(?:(?:\+?1\s*(?:[.-]\s*)?)?(?:\(\s*([2-9]1[02-9]|[2-9][02-8]1|[2-9][02-8][02-9])\s*\)|([2-9]1[02-9]|[2-9][02-8]1|[2-9][02-8][02-9]))\s*(?:[.-]\s*)?)?([2-9]1[02-9]|[2-9][02-9]1|[2-9][02-9]{2})\s*(?:[.-]\s*)?([0-9]{4})(?:\s*(?:#|x\.?|ext\.?|extension)\s*(\d+))?$</code></td>
    </tr>
  </tbody>
</table>

#### `required` 属性

如果`required`属性出现，那么表单在能够提交前必须包含有效信息。例如：使邮编地址被要求，我们会简单地加上`required`属性:

{% highlight html %}
<input type="text" required pattern="^\d{5,6}(?:[-\s]\d{4})?$" ...>
{% endhighlight %}

#### `min`, `max` and `step` 最小、最大和步骤属性

对于数字输入类型，像数字或范围，还有日期或时间输入，当滑动和缩放调整时，你能够详细阐述它们的最小值和最大值。同样地，也能够详细阐述它们每一个需要增加或减少多少。例如：一双鞋子的尺寸应该设置一个最小值1和一个最大值13，调整间隔0.5。

{% highlight html %}
<input type="number" min="1" max="13" step="0.5" ...>
{% endhighlight %}

#### `maxlength` 最大长度属性

`maxlength` 属性能够被用来说明一个输入框或文本框的最长字符长度。并且在当你想限制用户提供的信息长度时，也非常有用。例如：假设你想限制一个文件名在12个字符以内，你可以使用如下所示语句：
{% highlight html %}
<input type="text" id="83filename" maxlength="12" ...>
{% endhighlight %}

#### `novalidate` 属性

在一些情况下，你可能想允许用户提交一个即使包含了无效输入的表单。那么给表单元素添加novalidate属性，或者添加单独的输入标签就可以办到。在这种情况下，如果表单验证了输入，所有的伪类和JavaScript APIs仍然会允许你检查。
In some cases, you may want to allow the user to submit the form even if it
contains invalid input. To do this, add the `novalidate` attribute to the form
element, or individual input fields. In this case, all pseudo classes and
JavaScript APIs will still allow you to check if the form validates.

{% highlight html %}
<form role="form" novalidate>
  <label for="inpEmail">Email address</label>
  <input type="email" ...>
</form>
{% endhighlight %}

{% include modules/remember.liquid title="Remember" list=page.remember.provide-real-time-validation %}

### 使用JavaScript以应对更复杂的实时认证

当内置认证加上正当表达式不够时，你可以使用[Constrains Validation API](http://dev.w3.org/html5/spec-preview/constraints.html#constraint-validation)，这是一款强有力的工具，用来管理自定义认证。API允许你设置一个自定义错误，检查元素是否有效，还有总结出一个元素无效的原因：

<table class="table-2 tc-heavyright">
  <thead>
    <tr>
      <th data-th="API">API</th>
      <th data-th="Description">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="API"><code>setCustomValidity()</code></td>
      <td data-th="Description">Sets a custom validation message and the <code>customError</code> property of the <code>ValidityState</code> object to <code>true</code>.</td>
    </tr>
    <tr>
      <td data-th="API"><code>validationMessage</code></td>
      <td data-th="Description">Returns a string with the reason the input failed the validation test.</td>
    </tr>
    <tr>
      <td data-th="API"><code>checkValidity()</code></td>
      <td data-th="Description">Returns <code>true</code> if the element satisfies all of it's constraints, and <code>false</code> otherwise.</td>
    </tr>
    <tr>
      <td data-th="API"><code>validity</code></td>
      <td data-th="Description">Returns a <code>ValidityState</code> object representing the validity states of the element.</td>
    </tr>
  </tbody>
</table>

#### 设置自定义认证信息

如果一个表单认证失败，那么使用`setCustomValidity()`来标记无效标单并且解释为什么表单无效。例如：一个注册表单可能会要求用户输入两次邮箱地址以确认他们的邮件地址。在第二次输入使用一个模糊事件以认证两次输入和设置合适的网页回应。例如：

{% include_code _code/order.html customvalidation javascript %}

#### 防止因表格无效而撤销

因为如果有无效数据，并不是所有的浏览器都会禁止用户提交表单。如果表单有效，你需要注意提交事件，以及给表单元素使用`checkValidity()`
来判断:

{% include_code _code/order.html preventsubmission javascript %}

### 显示实时反馈

在用户提交表单前否准确地完成了表单的情况下提供视觉提示是很有帮助的。HTML5同样地也提供了一系列的伪类，以值和属性为基础，从而确定输入样式。

<table class="table-2 tc-heavyright">
  <thead>
    <tr>
      <th data-th="Pseudo-class">Pseudo-class</th>
      <th data-th="Use">Use</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Pseudo-class"><code>:valid</code></td>
      <td data-th="Use">Explicitly sets the style for an input to be used when the value meets all of the validation requirements.</td>
    </tr>
    <tr>
      <td data-th="Pseudo-class"><code>:invalid</code></td>
      <td data-th="Use">Explicitly sets the style for an input to be used when the value does not meet all of the validation requirements.</td>
    </tr>
    <tr>
      <td data-th="Pseudo-class"><code>:required</code></td>
      <td data-th="Use">Explicitly sets the style for an input element that has the required attribute set.</td>
    </tr>
    <tr>
      <td data-th="Pseudo-class"><code>:optional</code></td>
      <td data-th="Use">Explicitly sets the style for an input element that does not have the required attribute set.</td>
    </tr>
    <tr>
      <td data-th="Pseudo-class"><code>:in-range</code></td>
      <td data-th="Use">Explicitly sets the style for a number input element where the value is in range.</td>
    </tr>
    <tr>
      <td data-th="Pseudo-class"><code>:out-of-range</code></td>
      <td data-th="Use">Explicitly sets the style for a number input element where the value is out of range.</td>
    </tr>
  </tbody>
</table>

当网页读取完毕，可能标签显示无效，甚至用户还没有开始输入，认证也会立即开始。这同时也意味着，当用户输入的时候，网页可能看到输入过程中的无效方式。为了防止这个情况，在用户已经访问标签的时候，你可以将CSS和JavaScript结合，只显示无效方式。

{% include_code _code/order.html invalidstyle css %}
{% include_code _code/order.html initinputs javascript %}

{% include modules/remember.liquid title="Important" list=page.remember.show-all-errors %}

{% include modules/nextarticle.liquid %}

{% endwrap %}
