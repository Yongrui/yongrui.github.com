---
layout: post
title: "无限翻页"
category: javascript
tags: [javascript, scroll, 无限翻页, 无限滚动]
comments: true
description: "<p>无限翻页非常适合展现零散的、实时推送和按时间排列的信息，在浏览大量条目时无限翻页更有效，但无限翻页并不是一个万全之策,所以我们需要考虑充分才能使用。其实对于搜索结果、长列表和电子商务来说，分页导航也许才是最好的选择。</p><p>分页导航几乎只是基于技术原因提出的：</p><ul><li>老版本浏览器渲染慢</li><li>客户端和服务器之间任何一处都可能有带宽限制,这要求我们减少页面大小</li><li>服务器端的处理时间随着数据增多而增加.一次性渲染整个数据集不仅是浪费,而且对服务器来说也不可行,尤其是服务器想要处理足够多的并发请求时</li></ul><p />"
---

无限翻页非常适合展现零散的、实时推送和按时间排列的信息，在浏览大量条目时无限翻页更有效，但无限翻页并不是一个万全之策,所以我们需要考虑充分才能使用。其实对于搜索结果、长列表和电子商务来说，分页导航也许才是最好的选择。

分页导航几乎只是基于技术原因提出的：

<ul>
<li>老版本浏览器渲染慢</li>
<li>客户端和服务器之间任何一处都可能有带宽限制,这要求我们减少页面大小</li>
<li>服务器端的处理时间随着数据增多而增加.一次性渲染整个数据集不仅是浪费,而且对服务器来说也不可行,尤其是服务器想要处理足够多的并发请求时</li>
</ul>

分页导航只不过是一种方法，一种不用JavaScript的方法。启用了JavaScript之后，如果用无限翻页比较合适的话，我们就可以不用任何分页链接，而用无限翻页来代替它们。

原理是首先判断文档底部离当前显示区域底部的距离不太远,然后在滚动条滚动到恰当的位置时载入更多内容，代码如下：

{% highlight javascript %}
// 判断是否已滚动到足够低
function lowEnougn() {
    var pageHeight = Math.max(document.body.scrollHeight, document.body.offsetHeight);
    var viewportHeight = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight || 0;
    var scrollHeight = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0;

    // 在离页面询问20像素时触发翻页
    return pageHeight - viewportHeight - scrollHeight < 20;
}

// 监测滚动位置并载入更多内容
function checkScroll() {
    if (!lowEnougn()) {
        return pollScroll();
    };

    // Do something
    // Load more contents with ajax or ...
    $.ajax({
        type: "GET",
        url: "example.php",
        success: function(msg) {
            // 添加内容
        },
        complete: pollScroll
    });
}

function pollScroll() {
    setTimeout(checkScroll, 100);
}

pollScroll();
{% endhighlight %}

上面的代码其实没有什么特别奇特的地方，实质上是在判断文档底部离当前显示区域底部是否足够低，然后频繁地检查垂直滚动条的当前状态，每秒10次！然后用Ajax载入更多内容。唯一比较棘手的就是跨浏览器正确计算长度比较麻烦，这从lowEnough()方法的代码中可以很明显地看到。

如果需要考虑到可用性和容错，也可以提供分页导航：把下一页链接设置为默认隐藏，如果Ajax获取数据失败就显示这些链接，这样用户还可以回到用分页链接来操作的状态。
