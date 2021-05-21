<template>
  <div>
    <h1>setup 完成父子通信</h1>
    <!-- <son :name="senData" >
    </son> -->

    <son :name="senData.val" @name-changed="changeName"></son>
  </div>
</template>

<script>
import {reactive} from 'vue'
// import {ref} from 'vue'
import son from './son'
  export default {
    name: 'father',
    components:{son},
    data() {
      return {
        
      }
    },
    setup(){
      // const senData = ref('这世界很酷')

      const senData =reactive({
        val:'senData'
      })
      setTimeout(() => {
        senData.val += 1
      }, 1000);
      function  changeName(){
        console.log('事件传送出来了')
      }
      return{
        senData,
        changeName
      }
    }
  }
</script>

<style lang="less" scoped>
  
</style>