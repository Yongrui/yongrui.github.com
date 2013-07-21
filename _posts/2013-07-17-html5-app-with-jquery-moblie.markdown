---
layout: post
title: "用jQuery Moblie开发HTML5移动应用"
category: HTML5
tags: ["HTML5", "jQuery Mobile", "移动应用"]
comments: true
description: ""
---

在不久前，我曾用不到一个月的时间去学习jQuery Mobile并开发出一款RSS新闻阅读器应用，我想说，它对于懂得jQuery的开发者来说，真的非常容易学，对于想学移动web app的初学者来说非常适合。

Jquery mobile是由（MT）Media Temple联合多家移动设备厂商以及软件企业共同发起的的针对触屏智能手机与平板电脑的website以及在线应用的前端开发框架，目前Jquery Mobile的最新稳定版本为已经为正式版1.3。Jquery mobile构建于Jquery ，为前端开发人员提供了一个兼容所有主流移动设备平台的统一UI接口系统。

###用jQuery Mobile开发HTML5应用的3个优点：

-   非常容易上手：如果你懂jQuery的话，通过阅读jQuery Mobile官方文档，一个星期你就可以掌握它，再用一些Ajax技术和写一些Javascript代码或者时jQuery代码你就可以去开发出一些初步可以工作的应用了，这相对开发原生的Android和IOS应用容易并且快多了。

-   支持跨平台和跨设备开发：jQuery Mobile一直致力于使“一个页面”能兼容所有的设备和平台，为了达到这个目标，jQuery Mobile的框架是基于渐进增强来构建的，所有的组件都设计为100%的width以兼容于弹性或响应式的布局。jQuery Mobile不仅在智能手机上，也设计和测试能够完全运行于平板电脑甚至桌面电脑。所以可以认为他为优先运行在移动设备上，而不是只运行于移动设备。

-   没有麻烦的应用商店审批过程：开发手机应用，尤其是开发iOS系统的手机应用，最痛苦的过程莫过于通过Apple应用商店的审批，想要让一个原生应用程序发布给iOS用户，你需要等待一个相当长的过程。而用jQuery Mobile开发应用则不用，由于JQuery Mobile应用程序仅仅是一种web应用程序，因此它继承了所有web环境的优点：当用户加载你的网站时，他们就马上“升级”到最新的版本，可以马上修复bug和添加新的特性，只要一个网址就可以，根本不用考虑IOS的DRM或者时Android的APK.

###用jQuery Mobile开发HTML5应用的3个缺点：

-   比原生应用运行速度慢：jQuery Mobile给我的最大不好的感觉就是比较慢，起码比原生的应用慢，首先它要加载jQuery库，然后再加载jQuery Mobile库，这导致了JQuery Mobile应用程序都会明显慢。不过以后硬件速度和浏览器会很快得到提升，性能也许很快就不会成为问题。

-   跨浏览器和跨平台的不同表现：jQuery Mobile现在还不是特别稳定，所以会有很多的bug。最大的问题莫过于不同浏览器在不同手机上出现的古怪表现。

-   不能访问设备的特性：毕竟jQuery Mobile只是运行在浏览器上的Javascript类库，很明显，它并不能访问设备上的特性，例如摄像头。然而，它也可以借助想PhoneGap这样的工具来弥补。

###总结：

总的来说，我认为可以用jQuery Mobile来进行开发一些它力所能及的应用，例如像一些内容显示和数据输入类型的应用程序。我相信在未来HTML5一定会是手机应用中的一种非常重要的技术，HTML5应用很有可能会赶上原生应用。
