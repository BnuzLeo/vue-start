# SLOT

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/template/slot/slot.html)
- 实现功能：
```text
两种方法实现父组件往子组件中传入DOM节点
1. 属性传值（不推荐）
2. Slot插槽使用 （推荐）
```

## 属性传值（不推荐）
- 思路（注意：这是一个错误例子）
```html
1. 声明组件
var childOne = {
	template: '<div>Hello {{content}}</div>'
}

2. 属性传入
<child-one content = '<p>Slot</p>'></child-one>

ps: 其实这样是不行的
这时候需要使用v-html属性,且需要使用一个div的挂载节点
<div>Hello <div v-html="this.content"></div></div>

还需要注意，这样也是不行的
<div>Hello <div>{{content}}</div></div>
```
总结： 这样就有一个问题了：
1. 如果短的dom节点还好，如果一大串的话，代码看起来就很臃肿
2. 每次都会多一个div节点，这不是我们需要的

## Slot插槽使用（推荐）
- 只有一个slot
```html
思路：
1. 声明组件
var childTwo = {
	template: '<div>Hello</div>'
}

2. 在节点中添加插槽
<child-two>
	<p>Slot</p>
</child-two>
ps：其实这个就是在节点之间插入DOM

3. 在组件中通过slot使用插槽
var childTwo = {
	template: '<div>Hello<slot></slot></div>'
}
```
- 默认slot
```html
1. 在节点中不添加插槽
<child-two></child-two>

2. 在组件中继续使用slot，并且添加默认的DOM
var childTwo = {
	template: '<div>Hello<slot><p>default</p></slot></div>'
}
ps: 这样的情况，最后显示的就是<p>default</p>
```

- 多个slot
```html
1. 使用插槽，并且添加slot属性，区分插槽
<child-three>
	<div slot="header">Header</div>
	<div slot="footer">Footer</div>
</child-three>

2. 一个组件使用多个插槽
var childThree = {
	template: '<div><slot name="header"></slot>Hello<slot name="footer"></slot></div>'
}
```
总结：这样就会显示
Header
Hello
Footer
