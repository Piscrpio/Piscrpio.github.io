---
title: Hexo_learn
date: 2017-07-26 11:25:47
tags: essay
---
# Hexo初次尝试

### 无序列表
- 文本列表1
- 文本列表2
- 文本列表3


### 有序列表
1. 文本列表1
2. 文本列表2
3. 文本列表3


### [简书](http://www.jianshu.com)


![timg (3).jpg](http://upload-images.jianshu.io/upload_images/3406013-29daeefecbd10561.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 一盏灯， 一片昏黄； 一简书， 一杯淡茶。 守着那一份淡定， 品读属于自己的寂寞。 保持淡定， 才能欣赏到最美丽的风景！ 保持淡定， 人生从此不再寂寞。


```
(function(doc, win) {

	var docEle = doc.documentElement,
		dpr = Math.min(win.devicePixelRatio, 3),
		scale = 1 / dpr,

		resizeEvent = 'orientationchange' in window ? 'orientationchange' : 'resize';

	var metaEle = doc.createElement('meta');
	metaEle.name = 'viewport';
	metaEle.content = 'initial-scale=' + scale + ',maximum-scale=' + scale;
	docEle.firstElementChild.appendChild(metaEle);

	var recalCulate = function() {
		var width = docEle.clientWidth;
		docEle.style.fontSize = 10 * (width / 750) + 'px';
	};

	recalCulate();

	if (!doc.addEventListener) return;
	win.addEventListener(resizeEvent, recalCulate, false);
})(document, window);
```
