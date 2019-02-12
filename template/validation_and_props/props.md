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