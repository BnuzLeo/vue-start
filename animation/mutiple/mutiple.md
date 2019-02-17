# 多个元素和组件的过渡

## 例子
- 参考代码：  
[多个元素的过渡](https://github.com/BnuzLeo/vue-start/blob/master/animation/mutiple/mutiple_properties.html)  
[多个组件的过渡](https://github.com/BnuzLeo/vue-start/blob/master/animation/mutiple/mutiple_template.html)
- 实现功能：
```text
1. 多个元素的过渡
2. 多个组件的过渡
```

## 多个元素的过渡
- html
```html
<div id="root">
	<transition mode="out-in">
	  <button v-if="isEditing" key="save" @click="clickSave">
	    Save
	  </button>
	  <button v-else key="edit" @click="clickEdit">
	    Edit
	  </button>
	</transition>
</div>
```
总结:
```
1. 过渡模式
in-out：新元素先进行过渡，完成之后当前元素过渡离开。
out-in：当前元素先进行过渡，完成之后新元素过渡进入。

2. 多个元素展示的case
- 方式1：
<transition>
  <button v-if="isEditing" key="save">
    Save
  </button>
  <button v-else key="edit">
    Edit
  </button>
</transition>

- 方式2：
在一些场景中，也可以通过给同一个元素的 key 特性设置不同的状态来代替 v-if 和 v-else，上面的例子可以重写为：
<transition>
  <button v-bind:key="isEditing">
    {{ isEditing ? 'Save' : 'Edit' }}
  </button>
</transition>

- 方式3：
使用多个 v-if 的多个元素的过渡可以重写为绑定了动态属性的单个元素过渡。例如：
<transition>
  <button v-if="docState === 'saved'" key="saved">
    Edit
  </button>
  <button v-if="docState === 'edited'" key="edited">
    Save
  </button>
  <button v-if="docState === 'editing'" key="editing">
    Cancel
  </button>
</transition>
这种形式可以重写为：
<transition>
  <button v-bind:key="docState">
    {{ buttonMessage }}
  </button>
</transition>

computed: {
  buttonMessage: function () {
    switch (this.docState) {
      case 'saved': return 'Edit'
      case 'edited': return 'Save'
      case 'editing': return 'Cancel'
    }
  }
}
```

- js
```js
var vm = new Vue({
	el: '#root',
	data: {
		isEditing: true
	},
	methods: {
		clickSave: function(){
			this.isEditing = false;
		},
		clickEdit: function(){
			this.isEditing = true;
		}
	}
})
```

- css
```css
.v-enter{
	opacity: 0;
}

.v-enter-active{
	transition: opacity 2s
}
```

## 多组件过渡[方式1]
- html
```html
<div id="root">
  <transition mode="out-in">
    <btn-one v-if="isEditing"></btn-one>
    <btn-two v-else></btn-two>
  </transition>
  <button @click="handleClick">Change</button>
</div>
```
- js
```js
Vue.component('btn-one',{
    template:"<button>btn-one</button>"
  })

  Vue.component('btn-two',{
    template:"<button>btn-two</buttonbutton>" 
  })

  var vm = new Vue({
    el: '#root',
    data: {
      isEditing: true
    },
    methods: {
      handleClick: function(){
        this.isEditing = !this.isEditing
      }
    }
  })
```
- css
```css
.v-enter{
  opacity: 0;
}

.v-enter-active{
  transition: opacity 2s
}
```

## 多组件过渡[方式2]
- html
```html
<transition mode="out-in">
  <component :is="component"></component>
</transition>
<button @click="handleClick">Change</button>
```

- js
```js
Vue.component('btn-one',{
  template:"<button>btn-one</button>"
})

Vue.component('btn-two',{
  template:"<button>btn-two</buttonbutton>" 
})

var vm = new Vue({
  el: '#root',
  data: {
    component: 'btn-one'
  },
  methods: {
    handleClick: function(){
      this.component = this.component == 'btn-one' ? 'btn-two' : 'btn-one'
    }
  }
})
```

- css
```css
.v-enter{
  opacity: 0;
}

.v-enter-active{
  transition: opacity 2s
}
```
