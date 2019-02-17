# Vue使用animatecss库

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/animation/basic/animatecss.html)
- 实现功能：
```text
1. Vue利用@keyframes实现自定义样式
2. Vue使用animate css库样式
```

## @keyframes实现
- Html
```html
<div id="root">
	<transition name="fade">
		<div v-show="show">Hello Animation</div>
	</transition>
	<button @click='handleClick'>Trigger</button>
</div>
```
- Js
```js
<script>
	var vm = new Vue({
		el: '#root',
		data: {
			show: true
		},
		methods: {
			handleClick: function(){
				this.show = !this.show
			}
		}
	})
	
</script>
```
- Css
```css
@keyframes bounce-in {
	0%{
		transform: scale(0);
	}
	50%{
		transform: scale(1.5);
	}
	100%{
		transform: scale(1);
	}
}

.fade-enter-active{
	transform-origin: left center;
	animation: bounce-in 1s;
}


.fade-leave-active{
	transform-origin: left center;
	animation: bounce-in 1s reverse;	
}
```
总结：
```
1. 使用css3 动画的方式实现动画。
2. 通过animation绑定bounce-in的动画
3. 注意这里需要使用transform-origin注明起点，不然会出现一些bug
```

## Vue 使用 animate css
- html
```html
<transition 
enter-active-class="animated swing"
leave-active-class="animated wobble">
	<div v-show="show">Hello Animate Css</div>
</transition>
<button @click='handleClick'>Trigger</button>
```

- js
```js
var vm = new Vue({
	el: '#root',
	data: {
		show: true
	},
	methods: {
		handleClick: function(){
			this.show = !this.show
		}
	}
})
```

- css
```css
<link rel="stylesheet" href="../../libs/animate.css" type="text/css">
```

- 总结
```
1. 引入animate.css库
2. 通过自定义过渡标签属性来引入animate.css的样式
```