# TEMPLATE BASE

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/template/template_base/template_base.html)
- 实现功能
```text
自定义模板并且使用
```

## Template的声明与使用
- 声明
```js
Vue.component('row',{
	data: function(){
		return {
			content: 'Hi, I am Leon'
		}
	},
	template: '<tr><td>{{content}}</td></tr>'
})
```
- 使用
```html
方法1：
<row></row>
方法2：
<td is='row'></td>
```
## Template的小bug
- 生成问题
```html
如果使用<row></row>会出现的问题，html会渲染成
<tr>
	<td>Hi I am Leon</td>
</tr>
<table>
	<tbody></tbody>
</table>
```
ps: 所以建议使用<td is='row'></td>这种方法