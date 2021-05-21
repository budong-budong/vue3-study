<template>
  <div>
    <h1>第二章</h1>
    <watchAndWatchEffect/>
    <h2>生命周期</h2>
    <p>vue2---vue3</p>
    <p>beforecreate --- setup</p>
    <p>create --setup</p>
    <p> beforeMount --- onBeforeMount</p>
    <p>mounted --- onMounted</p>
    <p>beforeUpdate --- onBeforUpdate</p>
    <p>upDated --- onUpdated</p>
    <p>beforeDestroy --- onBeforeUnmount</p>
    <p>destroyed --- onUnmounted</p>
    <p>actived ---onActivated</p>
    <p>deactivated --- onDeativated</p>
  </div>
  <h2>如何使用axios</h2>
  <p>安装 vue add axios</p>
  <p>删除 mian.js import './plugins/axios</p>
  <p> 使用 import axios from "axios";</p>
  <todoList/>
</template>

<script>
import todoList from '../pages/todoList/index'
import { onBeforeMount,ref, onBeforeUnmount, onBeforeUpdate, onErrorCaptured, onMounted, onRenderTracked, onRenderTriggered, onUpdated } from 'vue'
import watchAndWatchEffect from '../pages/watchAndWatchEffect/index'
  export default {
    name: 'second',
    components:{watchAndWatchEffect,todoList},
    data() {
      return {
        
      }
    },
    // setup 相当于vue2中的beforecreate 和 created 并在两者之前执行
    setup(){
      let test = ref('测试')
      // 挂载开始之前被调用
      onBeforeMount(() =>{
        console.log('挂载开始之前被调用onBeforeMount',test);
      })
      // 实例被挂载后调用，不会保证所有的子组件也被挂载完
      onMounted(() =>{
        console.log('实例被挂载后调用，不会保证所有的子组件也被挂载完onMounted',test);
      })
      // dom更新前
      onBeforeUpdate(() =>{
        console.log('dom更新前onBeforeUpdate',test);
      })
      // dom更新后，不会保证所有的子组件也都一起被重绘
      onUpdated(() =>{
        console.log('dom更新后，不会保证所有的子组件也都一起被重绘onUpdated',test);
      })
      // 卸载组件实例之前，此时实例任然是完全正常的
      onBeforeUnmount(() =>{
        console.log('卸载组件实例之前，此时实例任然是完全正常的onBeforeUnmount',test);
      })
      // 卸载组件实例后调用，调用此钩子时，组件实例的所有指令都被解除绑定，所有的时间侦听器都被移除，所有的子组件实例被卸载
      onMounted(() =>{
        console.log('卸载组件实例后调用，调用此钩子时，组件实例的所有指令都被解除绑定，所有的时间侦听器都被移除，所有的子组件实例被卸载onMounted',test);
      })
      // 当捕获一个来自孙组件的错误时被调用
      onErrorCaptured(() =>{
        console.log('当捕获一个来自孙组件的错误时被调用onErrorCaptured',test);
      })
      // 跟踪虚拟dom重新渲染时调用
      onRenderTracked(() =>{
        console.log('跟踪虚拟dom重新渲染时调用onRenderTracked',test);
      })
      // 当虚拟 DOM 重新渲染为 triggered.Similarly 为renderTracked，接收 debugger event 作为参数。此事件告诉你是什么操作触发了重新渲染，以及该操作的目标对象和键。
      onRenderTriggered(() =>{
        console.log('当虚拟 DOM 重新渲染为 triggered.Similarly 为renderTracked，接收 debugger event 作为参数。此事件告诉你是什么操作触发了重新渲染，以及该操作的目标对象和键。onRenderTriggered',test);
      })
      return{test}
    }
  }
</script>

<style lang="less" scoped>
  
</style>