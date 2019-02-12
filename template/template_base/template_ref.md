# TEMPLATE REFS

## 例子
- 参考代码：[code]()
- 实现功能
```text
点击Copy按钮，复制 'Hi, I am Leon'
```

## ref的使用思路
- 自定义template
```js
Vue.component('ref',{
	data: function(){
		return {
			content: 'Hi, I am Leon'
		}
	},
	template: '<div>{{content}}</div>'
})
```
- 给自定义的template绑定ref属性
```html
<ref ref="introduction"></ref>
```
- 获取ref
```
this.$refs.introduction.content
```
ps: 在$refs里面获取的ref是一个引用，可以直接获取该引用中data的值