# PROPS

## 例子
- 动态组件：[code](https://github.com/BnuzLeo/vue-start/blob/master/template/dynamic_component_and_v-once/dynamic.html)
- v-once指令： [code](https://github.com/BnuzLeo/vue-start/blob/master/template/dynamic_component_and_v-once/v-once.html)
- 实现功能：
```text
点击Change按钮，切换child-one和child-two组件。
```

## 动态组件
- 实现
```html
1. 创建组件
Vue.component('child-one',{
	template: '<div>child-one</div>'
})

Vue.component('child-two',{
	template: '<div>child-two</div>'
})

2. 使用component标签以及is指令
<component :is="type"></component>

3. 创建按钮以及绑定handleClick事件
<button @click="handleClick">Change component</button>

4. 实现方法
methods: {
	handleClick: function(){
		this.type = this.type === 'child-one' ? 'child-two' : 'child-one';
	}
}
```
总结：这种方法简单易读。可以轻松切换组件

## v-once指令
```html
1. 创建组件
Vue.component('child-one',{
	template: '<div v-once>child-one</div>',
	mounted:function(){
		console.log('child-one created');
	}
})

Vue.component('child-two',{
	template: '<div v-once>child-two</div>',
	mounted:function(){
		console.log('child-two created');
	}
})

2. 使用组件以及创建按钮
<child-one v-if="type === 'child-one'"></child-one>
<child-two v-if="type === 'child-two'"></child-two>
<button @click="handleClick">Change component</button>

3. 实现方法
methods: {
	handleClick: function(){
		this.type = this.type === 'child-one' ? 'child-two' : 'child-one';
	}
}
```
总结：
1. 这种方法实现了和上面一样的功能。
2. 这里使用了v-once指令，这种指令可以在DOM创建之后放到内存中，然后下次切换的时候直接从内存中取出，这样可以大大调高效率。
3. 通常用于一些静态组件的使用。