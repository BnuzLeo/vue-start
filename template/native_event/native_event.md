# NATIVE EVENT

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/template/native_event/native_event.html)
- 实现功能：
```text
给组件绑定原生事件的两种实现方法
```

## 方法一
- 注意
```html
声明一个组件：
var child = {
	template: '<div>Click</div>',
}

使用组件并且绑定事件：
<child @click="handleClick"></child>

事件方法实现：
methods: {
	handleClick: function(){
		alert("Hello Native Event")
	}
}
```
- ps  
你会发现，这个click事件并没有执行 
- 原因  
这样写等于在父组件中监听child子组件的一个叫click的自定义事件，然而这个事件没有在子组件中声明和发射出来，所以是无法执行的。 
- 解决方案： 
```html
声明一个组件：
var child = {
	template: '<div @click="handleClick">Click</div>',
	methods:{
		handleClick:function(){
			this.$emit('click')
		}
	}
}

使用组件并且绑定事件：
<child @click="handleClick"></child>

事件方法实现：
methods: {
	handleClick: function(){
		alert("Hello Native Event")
	}
}
```
ps: 这样外部方法就可以实现了，但是这样写实在是太麻烦了，所以建议使用方法二

## 方法二
- 声明组件
```html
var childOne = {
	template: '<div>Click</div>'
}
```
- 使用native关键字给组件绑定原生事件
```html
<child-one @click.native="handleClick"></child-one>
```
- 实现事件
```html
methods: {
	handleClick: function(){
		alert("Hello Native Event")
	}
}
```
- 这样就大功告成啦

