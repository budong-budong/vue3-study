<template>
  <div>
    <h2>
      watch,WatchEffect 数据监听
    </h2>
     <p>{{ msg }}</p>
    <p>{{ msg2 }}</p>
    <p>{{ info }}</p>
    <p>
      <button @click="changeMsg">changeMsg</button>
    </p>
    <p>
      <button @click="changeMsg2">changeMsg2</button>
    </p>

    
  </div>
</template>

<script>
import { reactive ,watch,watchEffect,toRefs} from 'vue'
  export default {
    name: 'watchAndWatchEffect',
    data() {
      return {
        
      }
    },
    setup(){
      const state = reactive({
        msg:'时光',
        msg2:'你好',
        changeMsg2:() =>{
          state.msg2 = '你好，旧时光'
        }
      })

      const changeMsg = () =>{
        state.msg = '时光，改变',
        info = '你好，改变'
      }
      let info = 'hello';
      watch(state,() =>{
        console.log('观察整个state中属性的变化',state.msg);
      })
      // 监听指定的信息
    watch(
      () => state.msg,
      (newVal, oldVal) => {
        console.log("01-msg的新值是:" + newVal + "-------旧值是:" + oldVal);
      }
    );
    // 监听多个属性（数组形式）
    watch([() => state.msg, () => state.msg2], (newVal, oldVal) => {
      console.log("02-msg的新值是:" + newVal + "-------旧值是:" + oldVal); // 02-msg的新值是:时光，你好,俞亮-------旧值是:时光,俞亮
    });
    // 不需要指定监听的属性
    watchEffect(() => {
      // 程序运行时，初始化就会执行一次，完成监听准备工作
      console.log("03-watchEffect监听 state 中数据变化：", state.msg); // 有点像computed计算属性，用到的数据发生改变才会执行
    });

    // 使用时，要把对象return出去，才能在template中使用
    return {
      ...toRefs(state),
      info,
      changeMsg,
    };
    }
  }
</script>

<style lang="less" scoped>
  
</style>