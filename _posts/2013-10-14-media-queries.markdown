---
layout: post
title: "媒体查询(Media Queries)"
category: css
tags: ["css", "Media Queries"]
comments: true
description: ""
---

在uc的校招笔试中竟然考到了有关响应式web设计的题目，而我却忘记了，看来还是要做好笔记啊！！！！！！！！

下面是基于目前流行手机设备的屏幕分辨率的媒体查询：

{% highlight javascript %}
/* Samsung Galaxy (portrait) */
@media screen and (max-width: 385px) {

}

/* Samsung Galaxy (landscape) */
@media screen and (max-width: 690px) {

}

/* iPhone and other smartphones (portrait) */
@media screen and (max-device-width: 320px) {

}

/* iPhone and other smartphones (landscape) */
@media screen and (max-device-width: 480px) {

}

/* iPad and other tablets (portrait) */
@media screen and (max-device-width: 768px) {

}

/* iPad and other tablets (landscape) */
@media screen and (max-device-width: 1024px) {

}

/* iPhone 5 (portrait) */
@media screen and (max-device-width: 568px) and (orientation: portrait) {

}

/* iPhone 5 (landscape) */
@media screen and (max-device-width: 568px) and (orientation: landscape) {

}
{% endhighlight %}

上面的媒体查询类型兼容iPhone, iPad, SamSung手机的横向和纵向分辨率。

***以上知识参考自[W3CPlus](http://www.w3cplus.com/css3/design-based-media-queries.html)***