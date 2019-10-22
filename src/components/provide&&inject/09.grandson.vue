<template>
  <div>
    <h5 :style="{color: themeColor}">孙组件</h5>
  </div>
</template>

<script>
import { inject, ref } from '@vue/composition-api'
export default {
  setup() {
    // 2. 调用 inject 函数时，通过指定的数据名称，获取到父级共享的数据
    const themeColor = inject('globalColor')

    const count = ref(0);

    // 3. 把接收到的共享数据 return 给 Template 使用
    return {
      themeColor,
      count
    }
  }
}
</script>