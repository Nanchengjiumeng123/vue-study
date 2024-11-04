<template>

    <p>Has published books:</p>
    <!-- 用的时候不用加()，因为它是计算属性 -->
    <span>{{ publishedBooksMessage }}</span>
  
  
    <!-- 方法调用 -->
    <!-- <p>{{ calculateBooksMessage() }}</p> -->
  
  
  </template>
  
  
  <script>
  
  export default {
    // 如果在模板中写太多逻辑，会让模板变得臃肿，难以维护。比如说，我们有这样一个包含嵌套数组的对象：
    data() {
      return {
        author: {
          name: 'John Doe',
          books: [
            'Vue 2 - Advanced Guide',
            'Vue 3 - Basic Guide',
            'Vue 4 - The Mystery'
          ]
        },
  
        firstName: 'John',
        lastName: 'Doe'
      }
    },
  
  
    // 计算属性（computed）是一种基于依赖关系自动更新的属性。它接收一个函数作为参数，该函数的返回值会被缓存起来，
    // 并在依赖的数据发生变化时自动更新。计算属性通常用于根据其他数据进行计算，并将计算结果作为属性暴露给模板使用‌
    // 因此，可以使用计算属性来描述依赖响应式状态的复杂逻辑。
  
    // 更改此应用的 data 中 books 数组的值后，可以看到 publishedBooksMessage 也会随之改变。
    // 在模板中使用计算属性的方式和一般的属性并无二致。Vue 会检测到 this.publishedBooksMessage 依赖于 this.author.books，
    // 所以当 this.author.books 改变时，任何依赖于 this.publishedBooksMessage 的绑定都将同时更新。
  
    computed: {
      // 一个计算属性的 getter
      // 这里定义了一个计算属性 publishedBooksMessage。注意，这是属性，不是方法，它是一种计算属性。所以用的时候不用加()
      publishedBooksMessage() {
        // `this` 指向当前组件实例
        return this.author.books.length > 0 ? 'Yes' : 'No'
      },
  
  
      // 为什么下面的计算属性永远不会更新，因为 Date.now() 并不是一个响应式依赖,
      now() {
        return Date.now()
      },
  
  
      // 计算属性默认是只读的。当你尝试修改一个计算属性时，你会收到一个运行时警告。只在某些特殊场景中你可能才需要用到“可写”的属性，你可以通过同时提供 getter 和 setter 来创建：
      // 计算属性的getter和setter参数固定，getter没有参数，setter只有一个参数。而方法的参数不限
      // 一般情况下，计算属性只使用getter方法，所以计算属性可以简写。
  
      // 比如想要更新firstName和lastName
      fullName: {
        // getter
        // get方法是当属性被读取时触发，在计算属性中，如果计算属性依赖没有发生改变（例子中this.a就是计算属性的依赖，
        // 只要this.a不发生改变，它就不会再次调用get方法），get只会调用一次，并且会将返回结果缓存起来。
        // get方法必须需要一个返回值，否者会报出错误,因为计算属性本质上就是需要返回一个结果。
        get() {
          return this.firstName + ' ' + this.lastName
        },
  
        // setter
        // 如果set方法没有改变get方法中的依赖（this.a)，则get方法不会再次调用，而是直接使用缓存值。
        set(newValue) {
          // 注意：我们这里使用的是解构赋值语法
          [this.firstName, this.lastName] = newValue.split(' ')
        }
      }
  
  
  
      // 1.Getter 不应有副作用​
      // 计算属性的 getter 应只做计算而没有任何其他的副作用，这一点非常重要，请务必牢记。举例来说，不要改变其他状态、
      //在 getter 中做异步请求或者更改 DOM！一个计算属性的声明中描述的是如何根据其他值派生一个值。因此 getter 的职责应该仅为计算和返回该值。
      // 在之后的指引中我们会讨论如何使用侦听器根据其他响应式状态的变更来创建副作用。
  
  
      // 2.避免直接修改计算属性值​
      // 从计算属性返回的值是派生状态。可以把它看作是一个“临时快照”，每当源状态发生变化时，就会创建一个新的快照。更改快照是没有意义的，
      // 因此计算属性的返回值应该被视为只读的，并且永远不应该被更改——应该更新它所依赖的源状态以触发新的计算。
  
  
    },
  
  
  
    // 注意到我们在表达式中像这样调用一个函数也会获得和计算属性相同的结果
    // 然而，不同之处在于计算属性值会基于其响应式依赖被缓存。一个计算属性仅会在其响应式依赖更新时才重新计算。这意味着只要 author.books 不改变，无论多少次访问
    //publishedBooksMessage 都会立即返回先前的计算结果，而不用重复执行 getter 函数。如上面的now()''
    methods: {
      calculateBooksMessage1() {
        return this.author.books.length > 0 ? 'Yes' : 'No'
      }
    }
  
    // computed VS methods
    //为什么需要缓存呢？想象一下我们有一个非常耗性能的计算属性 list，需要循环一个巨大的数组并做许多计算逻辑，并且可能也有其他计算属性依赖于 list。
    // 没有缓存的话，我们会重复执行非常多次 list 的 getter，然而这实际上没有必要！如果你确定不需要缓存，那么也可以使用方法调用。
  
  
  }
  
  
  </script>
  