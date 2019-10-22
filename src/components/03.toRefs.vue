<template>
  <div>
    <p>{{ count }}</p>
    <button @click="add">加一</button>
  </div>
</template>

<script>
import { reactive, toRefs } from '@vue/composition-api'
export default {
  setup () {
    const state = reactive({ count: 0, name: "ljw" });
    // 定义自增函数
    const add = () => {
      state.count++;
    }

    // 在 setup 中返回一个对象供页面使用
    // 这个对象中可以包含响应式的数据，也可以包含事件处理函数
    return {
      // 对reactive函数定义的响应式数据对象使用展开运算符之后，
      // 会使响应式数据转为固定数据
      // ...state

      // 使用toRefs() 函数可以将 reactive() 创建出来的响应式对象，转换为普通的对象，
      // 只不过，这个对象上的每个属性节点，都是 ref() 类型的响应式数据
      ...toRefs(state),  // 将reactive（）创建出来的响应式对象转为ref（）类型的响应式数据
      add
    }
  }
}
</script>