<template>
  <div>
    <h3 :style="{color: themeColor}">子组件</h3>

    <hr>

    <son-com ref="comRef"/>
  </div>
</template>

<script>
// 1. 按需导入 inject
import { inject, ref } from '@vue/composition-api'

import SonCom from './09.grandson'
export default {
  components: {
    "son-com": SonCom
  },
  setup() {
    // 调用 inject 函数时，通过指定的数据名称，获取到父级共享的数据
    const themeColor = inject('globalColor')

    const str = ref('hello, world');

     // 1. 创建一个组件的 ref 引用
    const comRef = ref(null)

    // 5. 展示子组件中 count 的值
    const showCom = () => {
      console.log(comRef.value.count)
    }


    // 把接收到的共享数据 return 给 Template 使用
    return {
      themeColor,
      str,
      comRef,
      showCom
    }
  }
}
</script>