# vue-studyRecords

1.React 和 Vue 有许多相似之处，它们都有：

一、使用 Virtual DOM
提供了响应式 (Reactive) 和组件化 (Composable) 的视图组件。
将注意力集中保持在核心库，而将其他功能如路由和全局状态管理交给相关的库。

二、运行时性能
React 和 Vue 都是非常快的，所以速度并不是在它们之中做选择的决定性因素。

优化
在 React 应用中，当某个组件的状态发生变化时，它会以该组件为根，重新渲染整个组件子树。

如要避免不必要的子组件的重渲染，你需要在所有可能的地方使用 PureComponent，或是手动实现 shouldComponentUpdate 方法。

然而，使用 PureComponent 和 shouldComponentUpdate 时，需要保证该组件的整个子树的渲染输出都是由该组件的 props 所决定的。如果不符合这个情况，那么此类优化就会导致难以察觉的渲染结果不一致。这使得 React 中的组件优化伴随着相当的心智负担。

在 Vue 应用中，组件的依赖是在渲染过程中自动追踪的，所以系统能精确知晓哪个组件确实需要被重渲染。你可以理解为每一个组件都已经自动获得了 shouldComponentUpdate，并且没有上述的子树问题限制。

Vue 的这个特点使得开发者不再需要考虑此类优化，从而能够更好地专注于应用本身。

三、HTML & CSS
React中渲染功能都依靠JSX。
Vue也支持JSX，但是默认推荐还是模板。

2.
<div id="app-2">
  <span v-bind:title="message">
    鼠标悬停几秒钟查看此处动态绑定的提示信息！
  </span>
</div>

let app2 = new Vue({
  el: '#app-2',
  data: {
    message: '页面加载于 ' + new Date().toLocaleString()
  }
})

v-bind:title 相当于绑定元素的title属性, 也可以写作<span :title="message">
（将这个元素节点的 title attribute 和 Vue 实例的 message property 保持一致）


3.api:
数据 ps：都不要用箭头函数，会导致this的指向问题
data
只接受function

let data = { a: 1 }

// 直接创建一个实例
let vm = new Vue({
  data: data
})
vm.a // => 1
vm.$data === data // => true

// Vue.extend() 中 data 必须是函数
let Component = Vue.extend({
  data: function () {
    return { a: 1 }
  }
})

props、propsData、methods、watch

computed 计算属性的结果会被缓存，除非依赖的响应式 property 变化才会重新计算

4.DOM
el