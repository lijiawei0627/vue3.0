<template>
  <div id="app">
    <!-- <com-setup name = 'ljw'/> -->
    <!-- <com-ref /> -->
    <!-- <com-torefs /> -->
    <!-- <computed-com /> -->
    <!-- <watch-com /> -->
    <!-- <watch-com2 /> -->
    <!-- <watch-com3 /> -->
    <h1>父组件</h1>

    <button @click="showNumber">打印子组件的str值和孙组件的count值</button>
    <!-- 点击 App.vue 中的按钮，切换子组件中文字的颜色 -->
    <button @click="themeColor='red'">红色</button>
    <button @click="themeColor='blue'">蓝色</button>
    <button @click="themeColor='orange'">橘黄色</button>

    <hr>

    <son-com ref="comRef"/>
  </div>
</template>

<script>
// 1. 按需导入 provide
import { provide, ref } from '@vue/composition-api'

// import SetUpCom from './components/01.setup'
// import RefCom from './components/02.ref'
// import ToRefsCom from './components/03.toRefs'
// import ComputedCom from './components/04.computed'
// import WatchCom from './components/05.watch'
// import WatchCom2 from './components/06.watch2'
// import WatchCom3 from './components/07.watch3'
import SonCom from './components/provide&&inject/09.son'
export default {
  name: 'app',
  components: {
    // "com-setup": SetUpCom,
    // "com-ref": RefCom,
    // "com-torefs": ToRefsCom,
    // "computed-com": ComputedCom,
    // "watch-com": WatchCom,
    // "watch-com2": WatchCom2,
    // "watch-com3": WatchCom3,
    "son-com": SonCom
  },
  setup () {
    // 一、共享普通数据
    //  App 根组件作为父级组件，通过 provide 函数向子级组件共享数据（不限层级）
    //  provide('要共享的数据名称', 被共享的数据)
    // provide('globalColor', 'red')

    // 二、共享ref响应式数据
    // 定义 ref 响应式数据
    const themeColor = ref('red')

    // 把 ref 数据通过 provide 提供的子组件使用
    provide('globalColor', themeColor)

    // 创建一个组件的 ref 引用
    const comRef = ref(null);

    const showNumber = () => {
      console.log(comRef.value)
      // 打印子组件中的响应式数据
      console.log(comRef.value.str);
      // 调用子组件中的函数
      comRef.value.showCom();
    }

    // setup 中 return 数据供当前组件的 Template 使用
    return {
      themeColor,
      comRef,
      showNumber
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
