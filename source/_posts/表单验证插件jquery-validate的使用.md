---
title: 表单验证插件jquery-validate的使用
date: 2017-07-02 20:31:05
tags:
- 插件
- 笔记
- 学习
categories:
- js
- web
---




# jQuery-valiedate插件的使用

## 属性
在表单元素中添加指定的属性，来告诉插件需要如何进行验证

### data-required
设置当前表单项为必填项！如果用户没有输入内容，则验证不通过

### data-trim
设置当前表单项在验证的时候，去掉左右两边的空格，然后进行验证传参

### data-pattern
为当前表单项设置一个验证使用的正则表达式，如果该正则表达式验证通过则表单项验证通过！

### data-conditional
为当前表单项设置一个条件，这个条件是一个函数，在验证的时候会调用这个函数，如果函数返回值为true，则验证通过，否则不通过

### data-description
为当前表单项提供验证提示信息，和description对象配合使用

### data-describedby
为提示信息指定显示位置！！！ 等于后面是需要显示位置的ID

## validate方法的参数介绍

### sendForm
用来设置，表单验证通过之后，是否自动提交表单。默认是true。


### 回调函数们！
1. valid  当表单内所有的表单元素都通过验证的时候，会调用该方法
2. invalid 当表单内有任意元素不通过，那么整个表单验证就不通过，就会调用该方法
3. eachField 当表单内任意一个元素进行验证的时候都会调用该方法！
4. eachValidField 当任意表单元素通过校验的时候，就会调用该方法
5. eachInvalideField 当任意表单元素不通过校验的时候，就会调用该方法

### onKeyUp
设置按键的时候，是否要进行验证   默认值false

### onBlur
设置失去焦点的时候，是否要进行验证   默认值false

### onChange 
设置内容改变的时候，是否要进行验证   默认值false   注意:onchange这个事件在失去焦点时才会触发

### onSubmit
设置表单被提交的时候，是否要进行验证   默认值true

### conditional 
可以用来设置条件验证的条件,  这是一个对象，对象里面包含好多个方法。
当表单中有通过data-conditional来指定条件验证的函数的时候，插件会自动来这个对象中找对应名称的方法，进行调用，如果该方法的返回值为true则验证通过，否则验证不通过
```javascript
conditional: {
	"isXX": function(){
		return ...
	},
	"isXXx": function(){
		return ...
	}
}
```
### description
这个参数中用来设置验证的提示信息，需要和data-description属性配合使用
data-description中指定的提示信息会在这个对象中进行查找！
```javascript
description: {
	//下面的这个名字就是要在data-description中指定的名字
	"名字": {
		requeired: "",   //在验证的时候，如果非空校验失败就会显示该内容
		pattern:"",		//在验证的时候，如果格式校验失败就会显示该内容
		conditional: "", //在验证的时候，如果条件校验失败就会显示该内容
		valid: ""  //在验证的时候，如果校验通过就会显示该内容
	}
}
```

##案例
```html

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<script src="jquery/jquery.min.js"></script>
	<script src="jquery-validate.min.js"></script>
	<style>
		p{
			display: none;
		}
		.error{
			color: red;
			border:1px solid red;
		}
		.success{
			color:green;
			border:1px solid green;
		}
	</style>
</head>
<body>
	<form> 
		<table>
			<tr>
				<td>
					<input type="text" name="username" data-trim data-required data-describedby="usernameinfo" data-description="username" data-conditional="isShuaiGe">
					<p id="usernameinfo" ></p>
				</td>
			</tr>
			<tr>
				<td>
					<input type="text" name="phonenumber" data-trim data-required data-describedby="phoneinfo" data-description="phone" data-pattern="\d{11}">
					<p id="phoneinfo"></p>
				</td>
			</tr>
		</table>
		<button id="btn">提交</button>
	</form>
</body>

<script>
	//// validate方法是注册一个验证事件
	$("form").validate({
		sendForm:false,
		valid:function(){
			//当整个表单通过验证的时候，会调用该回调方法
			console.log("验证通过");
		},
		//当整个表单没有通过验证的时候，会调用该回调方法
		invalid:function(){
			console.log("验证没有通过");
		},
		//提交时每个表单元素都会调用该回调方法,this指向该表单元素
		eachField:function(){
			console.log("eachField被调用了",this);
		},
		eachValidField:function(){
			console.log("eachValidField被调用了",this);
			this.next().show().removeClass("error").addClass("success");
		},
		eachInvalidField:function(){
			console.log("eachInvalidField被调用了",this);
			this.next().show().removeClass("success").addClass("error");
		},
		conditional:{
			"isShuaiGe":function(){
				return this.val()=="傻叉";
			}
		},
		description:{
			"username":{
				required:"用户名不能为空",
				valid:"输入正确",
				conditional:"你输入的不是帅哥"
			},
			"phone":{
				required:"手机号码不能为空",
				valid:"输入正确",
				pattern:"手机号输入不正确"
			}
		}
	})
</script>
</html>

```