<template>
  <div>
    <h3 ref="h3Ref">TemplateRefOne</h3>
  </div>
</template>

<script>
// 通过 ref() 还可以引用页面上的元素或组件。
// 组件的引用与元素引用的用法一样（当拿到一个子组件之后，可以获取到子组件中的值）
// 具体参考components/provide&&inject/
import { ref, onMounted } from '@vue/composition-api'

export default {
  setup() {
    // 创建一个 DOM 引用
    const h3Ref = ref(null)

    // 在 DOM 首次加载完毕之后，才能获取到元素的引用
    onMounted(() => {
      // 为 dom 元素设置字体颜色
      // 注意：h3Ref.value 才是原生DOM对象，而不是h3Ref
      h3Ref.value.style.color = 'red'
    })

    // 把创建的引用 return 出去
    return {
      h3Ref
    }
  }
}
</script>