# 列表过渡

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/animation/list_transition/list_transition.html)
- 实现功能：
```text
列表过渡
```

## 使用思路
- html
```html
<div id="root">
	<transition-group mode="out-in">
	  <div v-for="item in items" :key="item.id">
	  	<div>{{item.name}}</div>	
	  </div>
	</transition-group>
	<button @click="add">Add</button>
</div>
```
总结
```html
1. 使用transition-group
2. 其实transition-group的原理就是：
<transition>
	<div>Hello list transition</div>
</transition>
<transition>
	<div>Hello list transition</div>
</transition>
<transition>
	<div>Hello list transition</div>
</transition>
```

- js
```js
var vm = new Vue({
	el: '#root',
	data: {
		items: []
	},
	methods: {
		add: function(){
			this.items.push({
				id: count++,
				name: 'Hello list transition'
			});
		}
	}
})
```

- css
```css
.v-enter{
	opacity: 0;
}

.v-enter-active{
	transition: opacity 2s
}
```