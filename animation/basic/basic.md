# Vue中css的动画原理

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/animation/basic/basic.html)
- 实现功能：
```text
点击Trigger按钮，使用过渡动画隐藏和显示Hello Animation字样。
```

## 使用
```html
1. DOM节点
<div id="root">
	<transition name="fade">
		<div v-show="show">Hello Animation</div>
	</transition>
	<button @click='handleClick'>Trigger</button>
</div>

2. 方法实现
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

3. 样式
.fade-enter,
.fade-leave-to{
	opacity: 0;
}

.fade-enter-active,
.fade-leave-active{
	transition: opacity 1s;
}
```

## 原理
![原理](https://github.com/BnuzLeo/vue-start/blob/master/animation/basic/principle.png)

- 原理
```
其实Vue就是通过动态添加class样式来实现过渡效果的
1. 在第一帧：添加fade-enter和fade-enter-active样式
2. 在第二帧：去到fade-enter样式，添加fade-enter-to样式
3. 在最后一帧： 去除fade-enter-active和fade-enter-to样式
```