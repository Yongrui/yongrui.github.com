---
layout: post
title: "忘记jQuery API，使用JS原生API"
category: javascript
tags: ["jQuery", "javascript"]
comments: true
description: ""
---

JavaScript已经为你准备好了，但你可能还没准备好使用它。为什么不使用jQuery? 因为它慢，并且你的网站并不是真的需要它的额外负重。

我并打算讨论库和原生，有时候缺少了不管哪一样，另一样都很难存活下来。但是我打算讨论一下 $ 代码的加载性能。

假设不考虑jQuery的易记性，每个人用jQuery是因为它支持IE，动画处理和那些选择器方法。

###原生的等价代码

选择元素

{% highlight javascript %}
// jQuery
var els = $('.el');

// Native
var els = document.querySelectorAll('.el');

// Shorthand
var $ = function (el) {
  return document.querySelectorAll(el);
}

var els = $('.el');
{% endhighlight %}

创建元素

{% highlight javascript %}
// jQuery
var newEl = $('<div/>');

// Native
var newEl = document.createElement('div');
{% endhighlight %}

添加事件监听器

{% highlight javascript %}
// jQuery
$('.el').on('event', function() {

});

// Native
[].forEach.call(document.querySelectorAll('.el'), function (el) {
  el.addEventListener('event', function() {

  }, false);
});
{% endhighlight %}

设置、获取属性

{% highlight javascript %}
// jQuery
$('.el').filter(':first').attr('key', 'value');
$('.el').filter(':first').attr('key');

// Native
document.querySelector('.el').setAttribute('key', 'value');
document.querySelector('.el').getAttribute('key');
{% endhighlight %}

添加、移除、切换类(class)

{% highlight javascript %}
// jQuery
$('.el').addClass('class');
$('.el').removeClass('class');
$('.el').toggleClass('class');

// Native
document.querySelector('.el').classList.add('class');
document.querySelector('.el').classList.remove('class');
document.querySelector('.el').classList.toggle('class');
{% endhighlight %}

添加(append)

{% highlight javascript %}
// jQuery
$('.el').append($('<div/>'));

// Native
document.querySelector('.el').appendChild(document.createElement('div'));
{% endhighlight %}

复制(clone)

{% highlight javascript %}
// jQuery
var clonedEl = $('.el').clone();

// Native
var clonedEl = document.querySelector('.el').cloneNode(true);
{% endhighlight %}

移除

{% highlight javascript %}
// jQuery
$('.el').remove();

// Native
remove('.el');

function remove(el) {
  var toRemove = document.querySelector(el);

  toRemove.parentNode.removeChild(toRemove);
}
{% endhighlight %}

父节点

{% highlight javascript %}
// jQuery
$('.el').parent();

// Native
document.querySelector('.el').parentNode;
{% endhighlight %}

前/后节点

{% highlight javascript %}
// jQuery
$('.el').prev();
$('.el').next();

// Native
document.querySelector('.el').previousElementSibling;
document.querySelector('.el').nextElementSibling;
{% endhighlight %}

XHR也叫做AJAX

{% highlight javascript %}
// jQuery
$.get('url', function (data) {

});
$.post('url', {data: data}, function (data) {

});

// Native

// get
var xhr = new XMLHttpRequest();

xhr.open('GET', url);
xhr.onreadystatechange = function (data) {

}
xhr.send();

// post
var xhr = new XMLHttpRequest()

xhr.open('POST', url);
xhr.onreadystatechange = function (data) {

}
xhr.send({data: data});
{% endhighlight %}

以上只是很少的一部分，你可以用浏览器的控制台找出更多的原生的东西，或者阅读[MDN’s JS API reference](https://developer.mozilla.org/ru/docs/Web/API)或者[WPD’s DOM docs](http://docs.webplatform.org/wiki/dom).

你也可以继续使用库，这里有一些[超轻量级的库](http://microjs.com/)，你可以用在你的项目上，但首先确定如果没有它们你就不能完成任务，如果否则的话请使用原生JS.

***[英文原文](http://blog.romanliutikov.com/post/63383858003/how-to-forget-about-jquery-and-start-using-native)***