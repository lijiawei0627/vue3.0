<template>
  <div>
    
  </div>
</template>

<script>
// watch() 函数用来监视某些数据项的变化，从而触发某些特定的操作
import { watch, ref, reactive } from '@vue/composition-api'
export default {
  setup () {
    const count = ref(0);
    // 定义 watch，只要 count 值变化，就会触发 watch 回调
    // watch 会在创建时会自动调用一次
    watch(() => console.log(count.value))
    // 输出 0

    setTimeout(() => {
      count.value++
      // 输出 1
    }, 1000)

    // 一、监视 reactive 类型的数据源：

    // 定义数据源
    const state = reactive({ count: 0 })
    // 监视 state.count 这个数据节点的变化
    // watch可以传两个参数，第一个是监视数据源，第二个执行函数
    watch(
      () => state.count,
      // count新值，prevCount旧值
      (count, prevCount) => {
        console.log(`${ count } --- ${ prevCount }`)
      },
      {
        lazy: true // 在 watch 被创建的时候，不执行回调函数中的代码
      }
    )


    // 二、监视 ref 类型的数据源：

    // 定义数据源
    const Refcount = ref(0)
    // 指定要监视的数据源
    // count新值，prevCount旧值
    watch(Refcount, (count, prevCount) => {
      console.log(`${ count } --- ${ prevCount }`)
    }, { lazy: true })


    // 三、监视多个数据源参考http://www.liulongbin.top:8085/#/?id=_93-%e7%9b%91%e8%a7%86%e5%a4%9a%e4%b8%aa%e6%95%b0%e6%8d%ae%e6%ba%90
    // 以数组形式传入，其他用法与前面一样
  }
}
</script>