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
```
<!-- 对象语法 (2.4.0+) -->
<button v-on="{ mousedown: doThis, mouseup: doThat }"></button>
```
##### keyCode 的事件用法已经被废弃了并可能不会被最新的浏览器支持。为了在必要的情况下支持旧浏览器，Vue 提供了绝大多数常用的按键码的别名
##### v-bind
```
<img :src="'/path/to/images/' + fileName">

<!-- class 绑定 -->
<div :class="{ red: isRed }"></div>
<div :class="[classA, classB]"></div>
<div :class="[classA, { classB: isB, classC: isC }]">
<!-- 绑定一个有属性的对象 -->
<div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>
<!-- 通过 $props 将父组件的 props 一起传给子组件 -->
<child-component v-bind="$props"></child-component>
```
##### v-model
限制：
```
<input>
<select>
<textarea>
components
```
修饰符：

- .lazy - 取代 input 监听 change 事件
- .number - 输入字符串转为有效的数字
- .trim - 输入首尾空格过滤
##### key
[作用]https://www.zhihu.com/question/61064119/answer/183717717
##### ref
预期：string

> ref 被用来给元素或子组件注册引用信息。引用信息将会注册在父组件的 $refs 对象上。如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例：
```
<!-- `vm.$refs.p` will be the DOM node -->
<p ref="p">hello</p>

<!-- `vm.$refs.child` will be the child component instance -->
<child-component ref="child"></child-component>
```
当 v-for 用于元素或组件的时候，引用信息将是包含 DOM 节点或组件实例的数组。

##### 关于 ref 注册时间的重要说明：因为 ref 本身是作为渲染结果被创建的，在初始渲染的时候你不能访问它们 - 它们还不存在！$refs 也不是响应式的，因此你不应该试图用它在模板中做数据绑定。
##### compute&watch的区别
> 使用 watch 选项允许我们执行异步操作 (访问一个 API)，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的
##### 插槽
它允许你像这样<b>合成组件</b>：
```
<navigation-link url="/profile">
  Your Profile
</navigation-link>
```
然后你在 <navigation-link> 的模板中可能会写为：
```
<a v-bind:href="url" class="nav-link">
  <slot></slot>
</a>
```
当组件渲染的时候，<slot></slot> 将会被替换为“Your Profile”。插槽内可以包含任何模板代码，包括 HTML：
```
<navigation-link url="/profile">
  <!-- 添加一个 Font Awesome 图标 -->
  <span class="fa fa-user"></span>
  Your Profile
</navigation-link>
```
甚至其它的组件：
```
<navigation-link url="/profile">
  <!-- 添加一个图标的组件 -->
  <font-awesome-icon name="user"></font-awesome-icon>
  Your Profile
</navigation-link>
```
> 如果 <navigation-link> 没有包含一个 <slot> 元素，则该组件起始标签和结束标签之间的任何内容都会被抛弃。
##### 生命周期
在实例初始化后
> beforCreate type:function

数据观察(data obersver),属性和方法的计算,event/watcher事件配置
> created type:function

> beforMount type:function

相关的render首次被调用
el还是 {{message}}，这里就是应用的 Virtual DOM（虚拟Dom）技术，
> mounted type:function

$el被vm.data替换并挂在在实例上后调用
<b>注意 mounted 不会承诺所有的子组件也都一起被挂载。如果你希望等到整个视图都渲染完毕，可以用 vm.$nextTick 替换掉 mounted</b>
```
mounted: function () {
  this.$nextTick(function () {
    // Code that will run only after the
    // entire view has been rendered
  })
}
```
数据更新
> beforeUpdate type:function

由于数据更新导致Dom重新渲染,这时候调用
> updated

<b>注意 updated 不会承诺所有的子组件也都一起被重绘。</b>
```
##### 在动态组件上使用 keep-alive
<!-- 失活的组件将会被缓存！-->
<keep-alive>
  <component v-bind:is="currentTabComponent"></component>
</keep-alive>
```
