<template>
    <!-- 文本插值 -->
    <!-- 双大括号标签会被替换为相应组件实例中 msg 属性的值。同时每次 msg 属性更改时它也会同步更新 -->
    <span>Message :{{ msg }} </span>
  
  
    <!-- 数据绑定 -->
    <!-- v-bind 指令指示 Vue 将元素的 id attribute 与组件的 dynamicId 属性保持一致。如果绑定的值是 null 或者 undefined，那么该 attribute 将会从渲染的元素上移除。 -->
    <!-- 简写： <div :id="dynamicId"></div>-->
    <div v-bind:id="dynamicId"></div>
  
  
    <!-- 绑定多个值 -->
    <!-- 通过不带参数的 v-bind，你可以将它们绑定到单个元素上 -->
    <div v-bind="objectOfAttrs"></div>
    <!-- const objectOfAttrs = {
    id: 'container',
    class: 'wrapper',
    style: 'background-color:green'
  } -->
  
  
    <!-- v-if -->
    <!-- v-on 简写：@-->
  
  
    <!-- 方法也可以在模板上被访问。在模板中它们常常被用作事件监听器： increment对应下面的方法，increment 方法会在 <button> 被点击时调用-->
    <button @click="increment">{{ count }}</button>
  
  
  
  
  
  </template>
  
  
  
  
  <script>
  
  
  export default {
    //  data 选项来声明组件的响应式状态。此选项的值应为返回一个对象的函数。Vue 将在创建新组件实例的时候调用此函数，
    // 并将函数返回的对象用响应式系统进行包装。此对象的所有顶层属性都会被代理到组件实例 (即方法和生命周期钩子中的 this) 上
  
    //  在 Vue 中，默认情况下，状态是深度响应的。这意味着当改变嵌套对象或数组时，这些变化也会被检测到
    data() {
      return {
        count: 1
      }
    },
  
    // `mounted` 是生命周期钩子，之后我们会讲到
    mounted() {
      // `this` 指向当前组件实例
      console.log(this.count) // => 1
  
      // 数据属性也可以被更改
      this.count = 2
  
  
  
    }
  }
  
  // 为组件添加方法
  methods: {
    increment() {
      this.count++
    }
  
    // Vue 自动为 methods 中的方法绑定了永远指向组件实例的 this。这确保了方法在作为事件监听器或回调函数时始终保持正确的 this。
    // 你不应该在定义 methods 时使用箭头函数，因为箭头函数没有自己的 this 上下文。
    // increment: () => {
    //    反例：无法访问此处的 `this`!
    // }
  
  
    // 当你修改了响应式状态时，DOM 会被自动更新。但是需要注意的是，DOM 更新不是同步的。Vue 会在“next tick”更新周期中缓冲所有状态的修改，以确保不管你进行了多少次状态修改，每个组件都只会被更新一次。
    // async increment() {
    //   this.count++
    //   await nextTick()
    //   现在 DOM 已经更新了，可以在此后面执行需要的代码
    // }
  }
  
  
  
  
  
  </script>
  
  <!-- Vue 在组件实例上暴露的内置 API 使用 $ 作为前缀。它同时也为内部属性保留 _ 前缀。因此，你应该避免在顶层 data 上使用任何以这些字符作前缀的属性 -->
  