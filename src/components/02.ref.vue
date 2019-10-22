<template>
  <div>
    <!-- 在setup函数外部会自动把响应式数据对象展开为原始的值，不需通过 .value 就可以直接被访问 -->
    <p>count的值为{{ count }}</p>
    <button @click="count++">加一</button>
  </div>
</template>

<script>
// ref() 函数用来根据给定的值创建一个响应式的数据对象，
// ref() 函数调用的返回值是一个对象，这个对象上只包含一个 .value 属性
import { ref } from '@vue/composition-api'
export default {
  // 在setup中创建的任何属性成员，都必须return出去，才能供template使用
  setup () {
    // 创建响应式数据对象 count，初始值为 0（能用ref创建响应式数据，尽量别用reactive）
    const count = ref(0);
    //  如果要访问 ref() 创建出来的响应式数据对象的值，必须通过 .value 属性才可以
    console.log(count.value); // 0
    // 让 count 的值 +1
    count.value++
    // 再次打印 count 的值
    console.log(count.value) // 输出 1
    // 必须以对象形式return出去
    return {
      count
    }

    // 当把 ref() 创建出来的响应式数据对象，挂载到 reactive() 上时，
    // 会自动把响应式数据对象展开为原始的值，不需通过 .value 就可以直接被访问
    // const count = ref(0)
    // const state = reactive({
    //   count
    // })

    // console.log(state.count) // 输出 0
    // state.count++ // 此处不需要通过 .value 就能直接访问原始值
    // console.log(count) // 输出 1
  }
}
</script>