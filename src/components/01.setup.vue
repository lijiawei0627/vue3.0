<template>
  <div>
    <!-- 在 template 中访问响应式数据 -->
    <p>{{ count }}</p>
    <button @click="count += 1">加一</button>
  </div>
</template>

<script>
// reactive() 函数接收一个普通对象，返回一个响应式的数据对象。
import { reactive } from '@vue/composition-api'
export default {
  // 通过 setup 函数的第一个形参，接收 props 数据：
  // setup 函数的第二个形参是一个上下文对象，
  // 这个上下文对象中包含了一些有用的属性attrs、slots、parent、root、emit、refs
  // 这些属性在 vue 2.x 中需要通过 this 才能访问到，在 vue 3.x 中，它们的访问方式如下：
  // 注意：在 setup() 函数中无法访问到 this
  setup (props, context) {
    console.log(props); // 'ljw'
    console.log(context.attrs)

    // reactive() 函数接收一个普通对象，返回一个响应式的数据对象。
    const state = reactive({ count: 0 });
    console.log(state);

    // setup 函数中必须将响应式数据对象 return 出去，才能供 template 使用
    return state
  },
  // 需要现在props声明
  props : {
    name: String
  }
}
</script>