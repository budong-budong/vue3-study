<template>
  <div>
    <h1>使用ref(torefs) 绑定数据</h1>
    <p>使用v-model双向绑定的数据是 {{msg}}</p>
    <p>
      <!-- 自己实现双向数据绑定，监听input事件，动态修改nmsg的值 -->
      <input type="text" ref="myInput" @input="input" :value="nmsg" />
    </p>
    <p>使用@input事件动态实现数据双向绑定数据的内容是：{{nmsg}}</p>
    <p>使用ref方法动态定义并双向数据绑定的hmsg是：{{hmsg}}</p>
    <p>torefs 来实现在模板中不需要追加state调用数据：{{msg}}</p>
  </div>
</template>

<script>
import {
  computed,
  getCurrentInstance,
  reactive,
  toRefs,
  defineComponent,
  ref,
} from 'vue'
export default defineComponent({
  name: 'ref',
  data() {
    return {}
  },
  setup() {
    const state = reactive({
      msg: '',
      nmsg: '',
      cmsg: computed(() => {
        return state.msg.length
      }),
    })

    const { ctx } = getCurrentInstance()
    const input = () => {
      // 在vue3 中，因为是面向hooks函数编程，所以无法通过this拿到当前vue实例对象
      console.log(ctx.$refs.myInput.value) // 像使用vue2中的this一样，使用ctx
      state.nmsg = ctx.$refs.myInput.value
    }

    const hmsg = ref('abc')
    const hmagInpu = () => {
      console.log('获取到的hsmg' + hmsg.value)
    }

    return {
      ...toRefs(state),
      hmsg,
      input,
      hmagInpu,
    }
  },
})
</script>

<style lang="less" scoped>
</style>