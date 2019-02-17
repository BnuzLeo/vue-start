# Vue的JS动画以及velocityjs的使用

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/animation/velocityjs/velocityjs.html)
- 实现功能：
```text
1. Vue的js动画的使用
2. Velocityjs的使用
```

## 使用思路
- 引入
```
<script src="../../libs/velocity.min.js"></script>
```

- html
```html
<div id="root">
	<transition 
	mode="out-in"
	@before-enter="beforeEnter",
	@enter="enter",
	@after-enter="afterEnter">
		<div v-if="show">Hello Velocity</div>
	</transition>
	<button @click="handleClick">Change</button>
</div>
```

- js
```js
var vm = new Vue({
	el:'#root',
	data: {
		show: true
	},
	methods: {
		handleClick: function(){
			this.show = !this.show
		},
		beforeEnter: function(el){
			el.style.opacity = 0;
		},
		enter: function(el,done){
			Velocity(
				el, 
				{opacity:1}, 
				{duration: 1000, complete: done}
				/*complete是Velocity要求的参数*/
			)
		},
		afterEnter: function(el){
			alert("Complete")
		}
}
```

- 总结
```
其实Vue的js动画就是用一些transition的生命周期钩子配合velocityjs来完成样式的改变。
```