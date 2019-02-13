# SLOT SCOPE

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/template/slot/scope_slot.html)
- 实现功能：
```text
由父组件决定子组件中循环的模式，使用"作用域卡槽"实现
```

## 作用域卡槽
- 思路
```html
1. 组件中准备数据
data:function(){
	return{
		list:[
			{
				id:1,
				name:"Leon"
			},{
				id:2,
				name:"Yannis"
			}
		]
	}
}

2. 在组件中循环数据，把数据通过属性传到父组件的卡槽中
template: 
`
	<div>
		<ul>
			<slot v-for="item of list" :item="item"></slot>
		</ul>
	</div>
`
总结：也就是说组件中只负责循环，你用什么形式展示由父组件决定

3. 父组件中通过teamplate占位标签和slot-scope属性使用作用域卡槽
<child>
	<template slot-scope="props">
		<li>{{props.item.id}} - {{props.item.name}}</li>
	</template>
</child>
总结 : 这里的思路是这样的
1. 先把组件中传过来的item放到props容器中，props的名字随便起的
2. 再通过{{props.item.**}}来使用
```