# 封装过渡组件

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/animation/package/package.html)
- 实现功能：
```text
封装过渡组件
```

## 使用思路
- html
```html
<div id="root">
	<fade :show="show">
		<div>封装组件</div>
	</fade>
	<fade :show="show">
		<H1>封装组件</H1>
	</fade>
	<button @click="handleClick">Change</button>
</div>
```

- js
```js
Vue.component('fade',{
	props:['show'],
	template:
	`
		<transition 
		@before-enter="handleBeforeEnter" 
		@enter="handleEnter">
			<slot v-if="show"></slot>
		</transition>
	`,
	methods: {
		handleBeforeEnter: function(el){
			el.style.color = 'red'
		},
		handleEnter: function(el, done){
			setTimeout(()=>{
				el.style.color = 'green'
				done()/*记得一定要手动执行done方法*/
			},2000)
		}
	}
})

var vm = new Vue({
	el: '#root',
	data:{
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
.v-enter,
.v-leave-to{
	opacity: 0
}

.v-enter-active,
.v-leave-active{
	transition: opacity 1s
}
```