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
`<div id="app-2">`  
  `<span v-bind:title="message">`  
    鼠标悬停几秒钟查看此处动态绑定的提示信息！  
 `</span>`  
`</div>`  
  
let app2 = new Vue({  
  el: '#app-2',  
  data: {  
    message: '页面加载于 ' + new Date().toLocaleString()  
  }  
})  

v-bind:title 相当于绑定元素的title属性, 也可以写作`<span :title="message">`
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

4.生命周期钩子 mounted渲染完之后调用

5.实例方法/事件：
1.on监听 emit触发
2.once 监听一个自定义事件，只触发一次。
3.off移除自定义事件监听器

  如果没有提供参数，则移除所有的事件监听器；

  如果只提供了事件，则移除该事件所有的监听器；

  如果同时提供了事件与回调，则只移除这个回调的监听器。

6.指令：
一、v-text 更新元素的textContent

示例：  
  
`<span v-text="msg"></span>`  
<!-- 和下面的一样 -->  
`<span>{{msg}}</span>`  

二、v-html 更新元素的innerHTML

在网站上动态渲染任意 HTML 是非常危险的，因为容易导致 XSS 攻击(??)。只在可信内容上使用 v-html，永不用在用户提交的内容上。

三、v-show 根据表达式之真假值，切换元素的 display CSS property。

四、v-if 根据表达式的值的 truthiness 来有条件地渲染元素。在切换时元素及它的数据绑定 / 组件被销毁并重建。如果元素是 `<template>`，将提出它的内容作为条件块。

五、v-else 限制：前一兄弟元素必须有 v-if 或 v-else-if。

六、v-for 基于源数据多次渲染元素或模板块。此指令之值，必须使用特定语法 alias in expression，为当前遍历的元素提供别名：
  
`<div v-for="item in items">`  
  {{ item.text }}  
`</div>`  

七、v-on 可以绑定一些事件的监听

八、v-bind 动态地绑定一个或多个 attribute，或一个组件 prop 的表达式。

九、v-model 限制：

`<input>、<select>、<textarea>、components`

十、v-slot

十一、v-pre 跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。

7.用 v-for 时加上 key 用来辨识虚拟DOM的节点 减少能耗。


****
`=======================================================================================  `  

Vue规范

优先级A：
1.组件名应为多个单词，内置组件除外。可以避免以后的名字重复。  
2.组件的 data 必须是一个函数。  
3.prop 的定义应该尽量详细。至少需要指定类型。  
4.为 v-for 设置 key 值。  
5.避免 v-for 与 v-if 同时用在同一个元素上， （为了过滤一个列表中的项目，为了避免渲染本应该被隐藏的列表）  
要么把if移动至容器元素上，要么先过滤列表之后再遍历过滤完的列表。  
6.为组件样式设置作用域。 scoped要慎用，scoped可以为当前的文件添加唯一性，会使引用此组件的组件很难去修改添加了scoped属性的组件的样式，所以如果组件的样式已经满足了所有情况且基本不需要修改才应加上scoped。所以不一定要使用 scoped attribute。设置作用域也可以通过 CSS Modules，那是一个基于 class 的类似 BEM 的策略，当然你也可以使用其它的库或约定。  
7.私有 property 名，使用模块作用域保持不允许外部访问的函数的私有性。  

优先级B：强烈推荐 (增强可读性)  
1.组件文件：只要有能够拼接文件的构建系统，就把每个组件单独分成文件。  
2.单文件组件的文件名应该要么始终是单词大写开头 (PascalCase)，要么始终是横线连接 (kebab-case)。
3.基础组件名：应用特定样式和约定的基础组件 (也就是展示类的、无逻辑的或无状态的组件) 应该全部以一个特定的前缀开头，比如 Base、App 或 V。
4.紧密耦合的组件名：和父组件紧密耦合的子组件应该以父组件名作为前缀命名。
比如：
components/  
|- TodoList.vue  
|- TodoListItem.vue  
|- TodoListItemButton.vue  
5.组件名中的单词顺序：组件名应该以高级别的 (通常是一般化描述的) 单词开头，以描述性的修饰词结尾。
动词—组件类型-描述性的修饰词
比如：
components/  
|- SearchButtonClear.vue  
|- SearchButtonRun.vue  
|- SearchInputQuery.vue  
|- SearchInputExcludeGlob.vue   
|- SettingsCheckboxTerms.vue  
|- SettingsCheckboxLaunchOnStartup.vue  
6.自闭合组件：在单文件组件、字符串模板和 JSX 中没有内容的组件应该是自闭合的——但在 DOM 模板里永远不要这样做。
7.组件名倾向完整单词而不是缩写。
8.Prop 名大小写：在声明 prop 的时候，其命名应该始终使用 camelCase，而在模板和 JSX 中应该始终使用 kebab-case。
比如：  
props: {
  greetingText: String
}
`<WelcomeMessage greeting-text="hi"/>`  
9.多个 attribute 的元素应该分多行撰写，每个 attribute 一行。
比如：  
`<MyComponent`  
`  foo="a"`  
`  bar="b"`  
`  baz="c"`  
`/>`  
10.指令缩写 (用 : 表示 v-bind:、用 @ 表示 v-on: 和用 # 表示 v-slot:) 应该要么都用要么都不用。