<template>


    <!-- 1-绑定对象 -->
    <!-- 可以给 :class (v-bind:class 的缩写) 传递一个对象来动态切换 class： -->
    <!-- active是属性，后面的是布尔值。true则属性存在，如下：active 是否存在取决于数据属性 isActive 的真假值。
    <div :class="active"></div> -->
    <div :class="{ active: isActive }"></div>
  
    <!-- :class 指令也可以和一般的 class attribute 共存，渲染的结果是：
  <div class="static active"></div>
  -->
    <div class="static" :class="{ active: isActive, 'text-danger': hasError }"></div>
  
  
    <!-- 绑定的对象并不一定需要写成内联字面量的形式，也可以直接绑定一个对象： <div class="active"></div>-->
    <div :class="classObject"></div>
  
  
    <!-- 2-绑定计算属性 -->
    <!-- 也可以绑定一个返回对象的计算属性。这是一个常见且很有用的技巧 -->
    <div :class="classComputedObject"></div>
  
  
    <!-- 3-绑定数组 结果：<div class="active text-danger"></div>-->
    <div :class="[activeClass, errorClass]"></div>
    <!-- 果你也想在数组中有条件地渲染某个 class，你可以使用三元表达式： errorClass 会一直存在，但 activeClass 只会在 isActive 为真时才存在。-->
    <div :class="[isActive ? activeClass : '', errorClass]"></div>
    <!-- 然而，这可能在有多个依赖条件的 class 时会有些冗长。因此也可以在数组中嵌套对象： -->
    <div :class="[{ [activeClass]: isActive }, errorClass]"></div>
  
  
    <!-- 样式绑定:style 支持绑定 JavaScript 对象值，对应的是 HTML 元素的 style 属性-->
    <div :style="{ 'font-size': fontSize + 'px' }"></div>
  
    <!--样式对象： 直接绑定一个样式对象通常是一个好主意，这样可以使模板更加简洁： -->
    <div :style="styleObject"></div>
  
    <!-- 同样，可以绑定数组 -->
    <div :style="[baseStyles, overridingStyles]"></div>
  
  
  </template>
  
  
  <script>
  
  export default {
    data() {
  
      // 当 isActive 或者 hasError 改变时，class 列表会随之更新。
      // 举例来说，如果 hasError 变为 true，class 列表也会变成 "static active text-danger"。
  
  
      // 我们在1-语法、响应式基础中提过：在 Vue 中，默认情况下，状态是深度响应的。这意味着当改变嵌套对象或数组时，这些变化也会被检测到
      // 因为vue使用了响应式系统来追踪数据变化，并自动更新视图
      return {
        isActive: true,
        hasError: false,
  
        // 对象
        classObject: {
          active: true,
          'text-danger': false
        },
  
        activeClass: 'active',
        errorClass: 'text-danger',
  
  
        // style-样式对象
        styleObject: {
          color: 'red',
          fontSize: '13px'
        }
  
  
  
      }
    },
  
  
    computed: {
      classComputedObject() {
        return {
          active: this.isActive && !this.error,
          'text-danger': this.error && this.error.type === 'fatal'
        }
      }
    }
  
  
  }
  
  </script>
  
  
  <style lang="css" scoped></style>
  