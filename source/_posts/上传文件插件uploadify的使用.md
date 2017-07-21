---
title: 上传文件插件uploadify的使用
date: 2017-07-03 19:18:27
tags:
- 学习
- 插件
- 笔记
categories:
- js
- web
---



# uploadify插件的使用总结

1. 引包
```html
	<link rel="stylesheet" href="uploadify/uploadify.css">
	<script src="jquery.js"></script>
	<script src="uploadify/jquery.uploadify.js"></script>
```

2. 调用uploadify提供的方法
```html
<input type="file" id="file">
```

```js
$("#file").uploadify({
	//指定swf文件的路径！！！ 推荐使用绝对路径
	swf: "/views/assets/uploadify/uploadify.swf",
	//指定上传文件的接口地址
	uploader: "/api/uploader/avatar",
	//指定上传文件的时候，文件的键， 后台需要通过该值来获取文件的内容
	fileObjName: "tc_avatar",
	//尺寸
	width: 100,
	height: 100,
	//类样式，附加一个类样式给上传按钮
	buttonClass: "类名",
	//按钮的文字
	buttonText: "上传图片",
	//设置上传图片的大小限制，可以是一个字符串,单位可以是B KB MB GB
	fileSizeLimit: "100KB",
	//设置上传文件的类型，也就是在选择文件的窗口中筛选指定类型的文件
	fileTypeExts: '*.gif; *.jpg; *.png',
	//formData  在上传文件的时候，可以附带一些数据，类似于ajax提交数据
	formData: {key: value},
	//设置上传进度的模板！
	itemTemplate : '<p></p>'
	//onUploadSuccess 上传成功之后的回调函数
	onUploadSuccess: function(file, data, response){
		
	},
	//onUploadComplete
	//onUploadError
	//onUploadProgress
	//onUploadStart
	//onUploadSuccess
});
```

