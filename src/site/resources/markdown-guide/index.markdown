---
layout: default
title: "Markdown指导"
description: "Markdown指导及本站所用语法。"
class: "page--styleguide"
learning-list:
  - Lorem ipsum dolor sit amet
  - Fugit itaque sapiente earum quo expedita
  - labore aliquam cupiditate veritatis nihil
article:
  written_on: 2014-01-01
  updated_on: 2014-01-06
  order: 3
collection: resources
key-takeaways:
  use-keytakeaway:
    - 添加一个重点很简单
remember:
  use-remember:
    - 添加一个记住很简单
related:
  related-content:
    - <a href="index.html">样式指导</a>
    - <a href="../example-article/">示例文章</a>
---
{% comment %}
注意：这是我们的样式指导
{% endcomment %}

{% wrap content %}

{% include modules/breadcrumbs.liquid %}

# {{ page.title }}

{% include modules/toc.liquid %}

## 标题

标题样式

# #一级标题

## ##二级标题

### ###三级标题

#### ####四级标题

##### #####五级标题

## 代码

如何将代码插入文档的样式。

### 无示例的的行内代码

  {{ "&#123;% highlight html %&#125;" }}

    <html>
        <head>
          <title>Hello World</title>
        </head>
    </html>

  {{ "&#123;% endhighlight %&#125;" }}

{% highlight html %}
<html>
  <head>
    <title>Hello World</title>
  </head>
</html>
{% endhighlight %}

### 插入Javascript

  {{ "&#123;% include_code _code/test.js testjs javascript %&#125;" }}

{% include_code _code/test.js somejs javascript %}


### 插入HTML

  {{ "&#123;% include_code _code/test.html testhtml html %&#125;" }}

{% include_code _code/test.html somehtml html %}


### 插入CSS

  {{ "&#123;% include_code _code/test.css testcss css %&#125;" }}

{% include_code _code/test.css somecss css %}

### 链接到示例

  {{ "&#123;% link_sample _code/test.html %&#125;See sample&#123;% endlink_sample %&#125;" }}

{% link_sample _code/test.html %}See sample{% endlink_sample %}

## 标注

在你的文档中使用标注轻而易举。

### 重点

    {{ "{% include modules/takeaway.liquid" }}
    	list=page.key-takeaways.use-keytakeaway %}

在你文章的YAML导言中

    key-takeaways:
	  use-keytakeaway:
	    - 添加一个重点很简单

{% include modules/takeaway.liquid list=page.key-takeaways.use-keytakeaway %}

### 记住

    {{ "{% include modules/remember.liquid" }}
    	list=page.remember.use-remember %}

在你文章的YAML导言中

    remember:
	  use-remember:
	    - 添加一个记住很简单

{% include modules/remember.liquid list=page.remember.use-remember %}


### 相关内容

    {{ "{% include modules/related.liquid" }}
      list=page.related.related-content %}

在你文章的YAML导言中

{% highlight yaml %}
related:
  related-content:
    - <a href="index.html">样式指导</a>
    - <a href="../example-article/">示例文章</a>
{% endhighlight %}

{% include modules/related.liquid list=page.related.related-content %}

{% endwrap %}
