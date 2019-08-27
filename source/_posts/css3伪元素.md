---
title: css3伪元素
date: 2017-08-14 14:03:10
categories: web
tags: [css,伪元素]
---

### css 伪元素 ::before ::after

#### 一、清除浮动
**元素增加zoom:1 兼容IE**
>Zoom属性是IE浏览器的专有属性， 它可以设置或检索对象的缩放比例
<!--more-->
伪元素增加 content display clear 属性 并且设置clear clear:both
给需要清楚浮动的父元素增加类就好了

```
.clearfix{zoom:1;} //兼容IE
.clearfix:after{ //在被选元素的内容后面插入内容。
    content:''; //content 属性来指定要插入的内容
    display:block;
    clear:both;
    font-size:0;
    height:0;
    visibility:hidden;
}

```


#### 二、前后动效

给菜单增加上下两条横线，缓冲出现


![img1.png](http://upload-images.jianshu.io/upload_images/3406013-0db49d3d15fff3c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![img2.png](http://upload-images.jianshu.io/upload_images/3406013-56aa100572954dcd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 首先先设置 主元素 定位属性 position:relative
- 然后设置 before after的属性 利用定位固定位置 加上 transition
- 最后 hover 设置经过的效果。

##### html
```
<ul class="text_ul clearfix">
      <li><a href="#" class="text">菜单</a></li>
      <li><a href="#" class="text">菜单</a></li>
      <li><a href="#" class="text">菜单</a></li>
      <li><a href="#" class="text">菜单</a></li>
      <li><a href="#" class="text">菜单</a></li>
</ul>
```


##### css
```
<style media="screen">
      *{
        margin: 0;
        padding: 0;
      }
      .clearfix:after {
         clear:both;
         content:".";
         display:block;
         font-size:0;
         height:0;
         visibility:hidden;
       }
      .clearfix:after {
         _zoom:1;
       }
      .text_ul{
        width: 500px;
        margin: 100px auto;
        background: pink;
        padding: 20px 0;
      }
      .text_ul li{
        float: left;
        list-style: none;
        width: 100px;
        text-align: center;
      }
      .text_ul li a{
        text-decoration: none;
        transition:all 1s ease 0s;
        position:relative;
        display: block;
        width: 100%;
      }
      .text::after,.text::before{
        content:'';
        overflow:hidden;
        display:inline-block;
        width:0px;
        height:1px;
        color:#fff;
        margin:1px auto;
        background-color:#333;
        transition:all 1s ease 0s;
        position:absolute;
      }
      .text:hover::after,.text:hover::before{
        width:100px;
      }
      .text::after{
        bottom:-5px;
        left:0;
      }
      .text::before{
        top:-5px;
        right:0;
      }

    </style>
```
