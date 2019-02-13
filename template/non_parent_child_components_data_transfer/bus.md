# NON PARENT CHILD COMPONENTS DATA TRANSFER

## 例子
- 参考代码：[code](https://github.com/BnuzLeo/vue-start/blob/master/template/non_parent_child_components_data_transfer/bus.html)
- 实现功能：
```text
点击Child1，改变Child2的属性。
点击Child2，改变Child1的属性。
1. 兄弟组件之间的传值。
2. 祖父和孙子之间的传值。
```

## 方法1：
- 思路
```
使用Vuex来实现非父子组件的传值。这里先不实现，但是是一个实现的思路。
```

## 方法2：
- 思路
```
1. 使用总线的机制完成非父子组件传值
也称为： BUS/总线/发布订阅模式/观察者模式
```

- 实现
```html
1. 创建两个兄弟组件
<child content="Bnuz"></child>
<child content="Leon"></child>	

2. 给Vue的prototype的bus绑定一个Vue实例
Vue.prototype.bus = new Vue()
ps : 其实这里是为了以后每个通过Vue创建出来的实例里面，都有一个Vue实例的bus

3. 给组件绑定监听器
template: '<div @click="handleClick">{{self}}</div>'

4. 给组件实现监听器
methods: {
	handleClick: function(){
		this.bus.$emit('change', this.self)
	}
}

5. 通过Mounted生命周期函数监听change事件
mounted: function(){
	var me = this
	this.bus.$on('change',function(msg){
		me.self = msg
	})
}
```