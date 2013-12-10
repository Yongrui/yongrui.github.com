---
layout: post
title: "Micro clearfix hack"
category: css
tags: ["css", "clearfix"]
comments: true
description: ""
---

clearfix hack是一个非常流行的不用添加多余的标签就可以清除浮动的方法。

支持的浏览器包括: Firefox 3.5+, Safari 4+, Chrome, Opera 9+, IE 6+ .

{% highlight css %}
.cf:before,
.cf:after {
    content: " ";
    display: table;
}

.cf:after {
    clear: both;
}

/**
 * 只针对IE 6/7
 * 这条规则会触发hasLayout属性和清除浮动
 */
.cf {
    *zoom: 1;
}
{% endhighlight %}

这个"micro clearfix"运用伪元素并设置```display: table```会生成一个匿名的表单元和新的block formatting context. ```:before```伪元素防止了top-margin倒塌下来；```:after```伪元素则是用于清除浮动。


包含```:before```对于清除浮动并不是必须的，但是它可以防止top-margin塌下来，和其他清除浮动的技术保持视觉一致性，例如：```overflow: hidden```

