### Vue.js
#### mounted
> 注意 mounted 不会承诺所有的子组件也都一起被挂载。如果你希望等到整个视图都渲染完毕，可以用 vm.$nextTick 替换掉 mounted：
```
mounted: function () {
  this.$nextTick(function () {
    // Code that will run only after the
    // entire view has been rendered
  })
}
```
##### 该钩子在服务器端渲染期间不被调用。
#### updated 
> 注意 updated 不会承诺所有的子组件也都一起被重绘。如果你希望等到整个视图都重绘完毕，可以用 vm.$nextTick 替换掉 updated：
```
updated: function () {
  this.$nextTick(function () {
    // Code that will run only after the
    // entire view has been re-rendered
  })
}
```
##### 该钩子在服务器端渲染期间不被调用。
##### parent
> 指定已创建的实例之父实例，在两者之间建立父子关系。子实例可以用 this.$parent 访问父实例，子实例被推入父实例的 $children 数组中。

##### 节制地使用 $parent 和 $children - 它们的主要目的是作为访问组件的应急方法。更推荐用 props 和 events 实现父子组件通信
##### mixins
类型：Array<Object>
详细：
> mixins 选项接受一个混入对象的数组。这些混入实例对象可以像正常的实例对象一样包含选项，他们将在 Vue.extend() 里最终选择使用相同的选项合并逻辑合并。举例：如果你的混入包含一个钩子而创建组件本身也有一个，两个函数将被调用。

Mixin 钩子按照传入顺序依次调用，并在调用组件自身的钩子之前被调用。

示例：
```
var mixin = {
  created: function () { console.log(1) }
}
var vm = new Vue({
  created: function () { console.log(2) },
  mixins: [mixin]
})
// => 1
// => 2
```
##### $watch
选项：deep

> 为了发现对象内部值的变化，可以在选项参数中指定 deep: true 。注意监听数组的变动不需要这么做。
```
vm.$watch('someObject', callback, {
  deep: true
})
vm.someObject.nestedValue = 123
// callback is fired
```
##### v-on修饰符
```
<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>
```
按键修饰符
> 在监听键盘事件时，我们经常需要检查详细的按键。Vue 允许为 v-on 在监听键盘事件时添加按键修饰符：
```
<!-- 只有在 `key` 是 `Enter` 时调用 `vm.submit()` -->
<input v-on:keyup.enter="submit">
```
>你可以直接将 KeyboardEvent.key 暴露的任意有效按键名转换为 kebab-case 来作为修饰符。
```
<input v-on:keyup.page-down="onPageDown">
```
##### keyCode 的事件用法已经被废弃了并可能不会被最新的浏览器支持。