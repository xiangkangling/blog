---
title: 图像裁剪插件Jcrop的使用
date: 2017-07-03 20:16:56
tags:
- 学习
- 插件
- 笔记
categories:
- js
- web
---

## 图像裁剪插件Jcrop的使用
#### 官网地址:官网地址:http://jcrop.org/ 
	 需要了解更多,可以参考这个官网的文档说明.
###插件的使用
1.引入文件包
```js
	<link rel="stylesheet" type="text/css" href="Jcrop/css/Jcrop.css">
	<!-- 这是一个基于jQuery写的插件,所以记得要先引入jquery.js -->
	<script src="jquery.js"></script>
	<script src="Jcrop/js/Jcrop.js"></script>
```
2.在页面中需要有一个img标签来引入需要裁切的图片,并且这个img需要有一个父级容器
```html
	<div id="container">
		<img src="2.jpeg" id="target">
	</div>
```
3.写js代码,实现裁切功能,并配置需要参数
```js
	<script>
		$(function(){
			$("#target").Jcrop({
				//盒子宽度设置
				boxWidth:600,
				//背景透明度设置
				bgOpacity:0.5,
				//选区的初始化参数[x坐标,y坐标,宽,高]
				setSelect:[0,0,200,200],
				//选区比例
				// aspectRatio: 2,	
				//背景色
				// bgColor: "hotpink",
				//选区最大尺寸
				// maxSize: [100, 100],
				//选区最小尺寸
				// minSize: [50, 50],
				//选区是否可以拖动改变
				// canSelect: false,
				//选区是否可以删除,只有当有多个选区的时候才有效果,默认值为true
				// canDelete:false,
				//选区是否能拖动
				// canDrag: false
				//选区是否能改变大小
				// canResize: false,
				//选区可选区域的边界值
				// edge: {n:10,s:10,e:10,w:10},
				// boxHeight: 100,
				// boxWidth: 1000,
				//是否可以有多个选框,默认为false
				// multi: true,
			//如果需要显示选区区域的预览图的时候,需要下面这个函数作为参数,
			},function(){
				// var jcrop_api = this;
				//console.log(this); //这里的width和height是设置预览区域的宽高
		  		thumbnail = this.initComponent('Thumbnailer', { width: 200, height: 150 });
			});

			//注册裁剪区域的移动事件
			$("#container").on('cropmove',function(e,s,c){
				//参数c是一个对象,里面包括选区的左上角和右下角的x,y坐标,还有选区的宽和高,
				//格式如下:Object {x: 175, y: 297.5, x2: 374.5, y2: 497.00000000000006, w: 199.5,h:199.5}
			  	console.log(c);
			});
		})
	</script>
```

