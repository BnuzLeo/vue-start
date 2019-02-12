# PROPS

## 例子
- 参考代码：[code]()
- 实现功能：
```text
通过属性给模板赋值
```

## 使用思路
- 通过标签属性传值
```html
<child content="Hello props"></child>
```
- 通过props来接收传值
```html
props: ['content'],
template:'<div>{{content}}</div>'
```

## Props特性
- Dom不显示
```html
<child content="Hello props"></child>
```
ps：一旦子子组件使用props来接收属性，在html里面显示是：
```html
<child></child>
```
- 子组件可以使用
```
props: ['content'],
template:'<div>{{content}}</div>'
```
ps: props接收之后，就可以在子组件中使用啦