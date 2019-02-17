# Vue中css的动画原理

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/animation/basic/basic.html)
- 实现功能：
```text
1. Vue实现过渡效果
2. 过渡效果原理
3. 过渡类名
4. 自定义过渡类名

```

## Vue实现过渡效果
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

## 过渡效果原理
![原理](https://github.com/BnuzLeo/vue-start/blob/master/animation/basic/principle.png)

- 原理
```
其实Vue就是通过动态添加class样式来实现过渡效果的
1. 在第一帧：添加fade-enter和fade-enter-active样式
2. 在第二帧：去到fade-enter样式，添加fade-enter-to样式
3. 在最后一帧： 去除fade-enter-active和fade-enter-to样式
```


## 过渡类名
- 注意
```html
这里有一个需要注意的点：
fade-enter,fade-enter-active,fade-enter-to的fade其实是transition标签的名字
<transition name="fade">
	<div v-show="show">Hello Animation</div>
</transition>
如果transition没有名字的话，就要使用v-enter,v-enter-active,v-enter-to
```
- 过渡类名
```
v-enter：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。

v-enter-active：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。

v-enter-to: 2.1.8版及以上 定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter 被移除)，在过渡/动画完成之后移除。

v-leave: 定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。

v-leave-active：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。

v-leave-to: 2.1.8版及以上 定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 v-leave 被删除)，在过渡/动画完成之后移除。
```

## 自定义过渡类名
- 自定义过渡类名
```
enter-class
enter-active-class
enter-to-class (2.1.8+)
leave-class
leave-active-class
leave-to-class (2.1.8+)
```
- Html
```html
<transition name="custom" 
enter-active-class="c-active" 
leave-active-class="c-leave" 
enter-class="c-enter"
leave-to-class="c-leave-to">
	<div v-show="show">Hello Animation</div>
</transition>
```
- css
```
/* 自定义过渡类名*/
.c-enter,
.c-leave-to{
	opacity: 0;
}
.c-active,
.c-leave{
	transition: opacity 1s;
}
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
