---
layout: post
title: "关于 repaint 和 reflow 一些介绍"
description: "<h3 id='_repaint__reflow'>什么是 repaint 和 reflow？</h3><p>一个页面由两部分组成：</p>
<ul><li>DOM：描述该页面的结构</li><li>render：描述 DOM 节点 (nodes) 在页面上如何呈现</li></ul><p>当 DOM 元素的属性发生变化 (如 color) 时, 浏览器会通知 render 重新描绘相应的元素, 此过程称为 repaint。</p><p>repaint(重绘)是在一个元素的外观被改变，但没有改变布局的情况下发生，如改变visibility、outline、前景色。</p><p>如果该次变化涉及元素布局 (如 width), 浏览器则抛弃原有属性, 重新计算并把结果传递给 render 以重新描绘页面元素, 此过程称为 reflow。</p><p>reflow(回流)是导致DOM脚本执行低效的关键因素之一。页面上任何一个结点触发reflow，都会导致它的子结点及祖先结点重新渲染。</p>"
category: 优化
tags: [reflow, repaint, 前端优化]
comments: true
---

###什么是 repaint 和 reflow？

一个页面由两部分组成：

-   DOM：描述该页面的结构
-   render：描述 DOM 节点 (nodes) 在页面上如何呈现

当 DOM 元素的属性发生变化 (如 color) 时, 浏览器会通知 render 重新描绘相应的元素, 此过程称为 repaint。

repaint(重绘)是在一个元素的外观被改变，但没有改变布局的情况下发生，如改变visibility、outline、前景色。

如果该次变化涉及元素布局 (如 width), 浏览器则抛弃原有属性, 重新计算并把结果传递给 render 以重新描绘页面元素, 此过程称为 reflow。

reflow(回流)是导致DOM脚本执行低效的关键因素之一。页面上任何一个结点触发reflow，都会导致它的子结点及祖先结点重新渲染。

###页面渲染的过程：
<p></p>
1.  解析HTML代码并生成一个 DOM 树。
2.  解析CSS文件，顺序为：浏览器默认样式->自定义样式->页面内的样式。
3.  生成一个渲染树（render tree）。这个渲染树和 DOM 树的不同之处在于，它是受样式影响的。它不包括那些不可见的节点。
4.  当渲染树生成之后，浏览器就会在屏幕上“画”出所有渲染树中的节点。

reflow 和 repaint 都是需要计算的，会消耗资源，影响用户体验。所有对用来生成渲染树的信息的改动都会触发 reflow 或者 repaint 。比如：添加或删除一个DOM节点、把一个节点的display设为none 等。由于reflow 和 repaint 会消耗资源，所以浏览器一般都会对此进行优化。有些浏览器会建立一个队列，把发生的 reflow 和 repaint 放进去，然后进行批处理。但是当你获取某些节点的样式信息的时候，会破坏浏览器的这种默认优化，强迫浏览器执行当前所有的 reflow 和 repaint。比如当你获取某个节点的 offsetTop 的时候，浏览器必须提供给你最新的数值，所以就需要把之前的 reflow 和 repaint 都执行。

###优化方法:

<p></p>
####1.  避免在document上直接进行频繁的DOM操作
<p></p>
-  先将元素从document中删除，完成修改后再把元素放回原来的位置
-  将元素的display设置为”none”，完成修改后再把display修改为原来的值
-  如果需要创建多个DOM节点，可以使用DocumentFragment创建完后一次性的加入document

<p></p>
####2.  集中修改样式
<p></p>
-  尽可能少的修改元素style上的属性
-  尽量通过修改className来修改样式
-  通过cssText属性来设置样式值

<p></p>
####3.  缓存Layout属性值

对于Layout属性中非引用类型的值（数字型），如果需要多次访问则可以在一次访问时先存储到局部变量中，之后都使用局部变量，这样可以避免每次读取属性时造成浏览器的渲染。

####4.  设置元素的position为absolute或fixed

在元素的position为static和relative时，元素处于DOM树结构当中，当对元素的某个操作需要重新渲染时，浏览器会渲染整个页 面。将元素的position设置为absolute和fixed可以使元素从DOM树结构中脱离出来独立的存在，而浏览器在需要渲染时只需要渲染该元素 以及位于该元素下方的元素，从而在某种程度上缩短浏览器渲染时间，这在当今越来越多的Javascript动画方面尤其值得考虑。

####5.  权衡速度的平滑

比如实现一个动画，以1个像素为单位移动这样最平滑，但reflow就会过于频繁，CPU很快就会被完全占用。如果以3个像素为单位移动就会好很多。

####6.  不要用tables布局

不要用tables布局的另一个原因就是tables中某个元素一旦触发reflow就会导致table里所有的其它元素reflow。在适合用table的场合，可以设置table-layout为auto或fixed，这样可以让table一行一行的渲染，这种做法也是为了限制reflow的影响范围

####7.  不要在css里面写expression

很多情况下都会触发reflow，如果css里有expression，每次都会重新计算一遍



***本文来自 [http://www.zhoonchen.com/](http://www.zhoonchen.com/blog/2011/05/%E5%85%B3%E4%BA%8Erepaint%E5%92%8Creflow%E4%B8%80%E4%BA%9B%E4%BB%8B%E7%BB%8D/)***
