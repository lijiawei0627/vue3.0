<template>
  <div>
    <p>count值为{{ count }}</p>
    <p>计算属性的值为{{ computedCount }}</p>
    <button @click="count++">加一</button>
  </div>
</template>

<script>
// computed() 用来创建计算属性，computed() 函数的返回值是一个 ref 的实例。
import { computed, ref } from '@vue/composition-api'
export default {
  setup () {
    const count = ref(0);
    // 根据 count 的值，创建一个响应式的计算属性computedCount
    // 它会根据依赖的 ref 自动计算并返回一个新的 ref

    // 在调用 computed() 函数期间，传入一个 function 函数，可以得到一个只读的计算属性
    const computedCount = computed(() => count.value + 1);

    // 在调用 computed() 函数期间，传入一个包含 get 和 set 函数的对象，
    // 可以得到一个可读可写的计算属性
    const plusOne = computed({
      // 取值函数
      get: () => count.value + 1,
      // 赋值函数
      set: val => {
        count.value = val - 1
      }
    })
    // 为计算属性赋值的操作，会触发 set 函数
    plusOne.value = 9
    // 触发 set 函数后，count 的值会被更新
    console.log(count.value) // 输出 8


    return {
      count,
      computedCount
    }
  }
}
</script>