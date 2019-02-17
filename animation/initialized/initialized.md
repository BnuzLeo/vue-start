# 初始渲染的过渡
## 例子
- 参考代码：  
[初始渲染的过渡](https://github.com/BnuzLeo/vue-start/blob/master/animation/initialized/initialized.html)
- 实现功能：
```text
1. 初始化渲染的过渡，就是页面一刷新就进入过渡渲染
```

## 使用思路
- html
```html
<div id="root">
<transition appear
			appear-class="custom-appear-class"
			appear-to-class="custom-appear-to-class"
			appear-active-class="custom-appear-active-class"
			v-on:before-appear="customBeforeAppearHook"
			v-on:appear="customAppearHook"
			v-on:after-appear="customAfterAppearHook"
			v-on:appear-cancelled="customAppearCancelledHook">
	<div v-if="show">初始渲染的过渡</div>
</transition>
<button @click="change">Change</button>
```
总结：
```
1. 可以通过 appear 特性设置节点在初始渲染的过渡

2. 这里默认和进入/离开过渡一样，同样也可以自定义 CSS 类名。
appear-class="custom-appear-class"
appear-to-class="custom-appear-to-class"
appear-active-class="custom-appear-active-class"

3. 自定义 JavaScript 钩子：
v-on:before-appear="customBeforeAppearHook"//出现之前
v-on:appear="customAppearHook"//正在出现
v-on:after-appear="customAfterAppearHook"//完全出现
v-on:appear-cancelled="customAppearCancelledHook"//出现的过程中取消
```

- js
```js
var vm = new Vue({
	el: '#root',
	data: {
		show: true
	},
	methods: {
		customBeforeAppearHook: function(){
			console.log("customBeforeAppearHook")
		},
		customAppearHook: function(){
			console.log("customAppearHook")
		},
		customAfterAppearHook: function(){
			console.log("customAfterAppearHook")
		},
		customAppearCancelledHook: function(){
			console.log("customAppearCancelledHook")
		},
		change: function(){
			this.show = !this.show
		}
	}
})
```

- css
```css
.custom-appear-class{
	opacity: 0
}

.custom-appear-active-class{
	transition: opacity 2s;
}

.custom-appear-to-class{
	opacity: 1
}
```