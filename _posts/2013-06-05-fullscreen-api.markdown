---
layout: post
title: "HTML5 Fullscreen Api"
description: "<p>HTML5给我们提供了全屏化的方法：Fullscreen API，其实就是一组简单的Javascript API。Fullscreen API给开发者提供了一种可编程化的方法将全屏种取消全屏的选择提供给用户，这在web应用和web游戏中是非常有用的。主要的API如下："
category: HTML5
tags: [HTML5, Javascript, FullscreenAPI]
comments: true
---

HTML5给我们提供了全屏化的方法：Fullscreen API，其实就是一组简单的Javascript API。Fullscreen API给开发者提供了一种可编程化的方法将全屏种取消全屏的选择提供给用户，这在web应用和web游戏中是非常有用的。主要的API如下：

###启动全屏
<p></p>
{% highlight javascript %}
// 某个元素的全屏化
element.requestFullScreen();
{% endhighlight %}

在不同的浏览器中使用需要添加前缀，例如写一个跨浏览器的requestFullScreen方法：

{% highlight javascript %}
function launchFullScreen(element) {
	if (element.requestFullScreen) { // W3C标准
            element.requestFullScreen();
    } eles if (element.webkitRequestFullScreen) { // Chrome/Safari
        element.webkitRequestFullScreen();
    } else if (element.mozRequestFullScreen) { // Firefox
        element.mozRequestFullScreen();
    }
}
    
// 调用launchFullScreen方法
launchFullScreen(document.documentElement); // 整个页面全屏化
launchFullScreen(document.getElementById("myVideoElement")); // 单个元素的全屏化
{% endhighlight %}

<p></p>
###退出全屏
<p></p>
{% highlight javascript %}
// 退出全屏化
document.cancelFullScreen();
{% endhighlight %}

和requestFullScreen一样，在不同的浏览器中使用需要添加前缀，例如写一个跨浏览器的cancelFullScreen方法：

{% highlight javascript %}
function cancelFullscreen() {
    if(document.cancelFullScreen) { // W3C标准
        document.cancelFullScreen();
    } else if(document.webkitCancelFullScreen) { // Chrome/Safari
        document.mozCancelFullScreen();
    } else if(document.mozCancelFullScreen) { // Firefox
        document.webkitCancelFullScreen();
    }
}
    
// 调用cancelFullScreen方法
cancelFullScreen();
{% endhighlight %}

<p></p>
###Fullscreen属性
<p></p>
{% highlight javascript %}
document.fullScreenElement // 返回全屏的元素，没有全屏则返回null
document.fullScreenEnabled // 标记或判断当前全屏是否可用
    
var fullscreenElement = document.fullscreenElement || document.mozFullScreenElement || document.webkitFullscreenElement;
var fullscreenEnabled = document.fullscreenEnabled || document.mozFullScreenEnabled || document.webkitFullscreenEnabled;
{% endhighlight %}

<p></p>
###Fullscreen事件

浏览器支持全屏事件 `fullscreenchange`，让开发者可以为全屏做更多事情：

{% highlight javascript %}
// Chrome/Safari
element.onwebkitfullscreenchange
    
// Firefox
element.onmozfullscreenchange
    
// W3C
element.addEventListener("fullscreenchange", function(e) {
    // To do something
}, false);
{% endhighlight %}

<p></p>
###Fullscreen CSS

浏览器也对Fullscreen CSS伪类提供了支持：

{% highlight css %}
/* html */
:-webkit-full-screen {
     background: pink;
}
:-moz-full-screen {
    background: pink;
}
    
/* elements */
:-webkit-full-screen video {
    width: 100%;
    height: 100%;
}
{% endhighlight %}
