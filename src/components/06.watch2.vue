<template>
  <div>
    <p>count值为 {{ count }}</p>
    <button @click="stopWatch">停止监视</button>
  </div>
</template>

<script>
import { watch, ref } from '@vue/composition-api'
export default {
  setup () {
    const count = ref(0);
    // 清除监视
    // 在 setup() 函数内创建的 watch 监视，会在当前组件被销毁的时候自动停止。
    // 如果想要明确地停止某个监视，可以调用 watch() 函数的返回值即可

    // 创建监视，并得到 停止函数
    const stop = watch(count, (count, prevCount) => {
      /* ... */
      console.log(`${count} --- ${prevCount}`)
    }, { lazy: true })


    setTimeout(() => {
      count.value++;
    }, 3000);
    // 调用停止函数，清除对应的监视
    // stop()
    function stopWatch () {
      stop();
    }
    return {
      count,
      stopWatch
    }
  }
}
</script>