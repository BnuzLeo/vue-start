# PROPS

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/template/validation_and_props/validation.html)
- 实现功能：
```text
poc各种props的validation的用法
```

## 使用思路
- 限制String类型
```
传值：
<valid-two :content="2"></valid-two>

使用：
var validTwo = {
	props: {
		content : String
	},
	template: '<div>{{content}}</div>'
}

提示：
[Vue warn]: Invalid prop: type check failed for prop "content". Expected String with value "2", got Number with value 2.
```

- 限制Number类型
```
传值：
<valid-three content="Hello validation three"></valid-three>

使用：
var validThree = {
	props: {
		content : Number
	},
	template: '<div>{{content}}</div>'
}

提示：
[Vue warn]: Invalid prop: type check failed for prop "content". Expected Number with value NaN, got String with value "Hello validation three"
```

- 同时限制String,Number类型
```
传值：
<valid-four :content="{'object':'1'}"></valid-four>

使用：
var validFour = {
	props: {
		content : [String, Number]
	},
	template: '<div>{{content}}</div>'
}

提示：
[Vue warn]: Invalid prop: type check failed for prop "content". Expected String, Number, got Object.

```

- 自定义属性
```
传值：
<valid-five></valid-five>

使用：
var validFive = {
	props:{
		content : {
			type : String,
			required : false,//是否必须
			default : 'Hello validation five',//默认值
			validator: function(value){//自定义validator
				return (value.length < 5)
			}
		}
	},
	template: '<div>{{content}}</div>'
}

提示：
[Vue warn]: Invalid prop: custom validator check failed for prop "content".
```
