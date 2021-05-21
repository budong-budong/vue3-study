<template>
  <div>
    <h1>注意 在setup函数中 无法访问到this!!!</h1>
    <h1>使用reactive绑定数据</h1>
    <p>{{state.msg}}</p>
    <p>{{info}}</p>
    <p>
      <button @click="changeMsg">changemsg</button>
    </p>
    <father ref="father"></father>
    <ref></ref>
    <h1>
      本章小结
    </h1>
    <h3>reactive</h3>
    <ol>
      <li>reactive方法，直接传入一个对象state，这个对象就是proxy拦截的对象</li>
      <li>然后再把这个state对象直接return出去就能被调用</li>
      <li>在temolate中使用state.msg来访问</li>
      <li>在js中也使用state.msg来访问</li>
    </ol>
    <h3>ref</h3>
    <ol>
      <li>使用ref直接声明一个proxy响应式对象msg</li>
      <li>然后把这个msg对象直接return出去</li>
      <li>在template中直接使用'{{msg}}'</li>
      <li>注意：在js中需要使用msg.value</li>
    </ol>
  </div>
</template>

<script>
import ref from '../pages/ref/index'
import father from '../pages/fatherAndSon/father'
import { defineComponent,reactive } from 'vue'
export default defineComponent({
  components: { father,ref },
  name: 'HelloWorld',
  setup(){
    const state = reactive({
      msg:'时光'
    })
    let info = 'hello'
    const changeMsg = () =>{
      state.msg = '时光，你好'
      info = 'hello 你好'
    }
    return{ //使用时，要把对象return出去，才能使用
      state,
      info,
      changeMsg
    }
  }
})

</script>


