<template>
  <div>
    <h1>todoList</h1>
    <h3>菜单列表</h3>
    <ul>
      <li v-for="(item,index) in list" :key="index">
        {{item.name}} 价格{{item.price}}
        <button @click="add(index)">点餐</button>
      </li>
    </ul>
    <h3>已点菜单</h3>
    <ul>
      <li v-for="(item,index) in aList" :key="index">
        {{item.name}} 价格{{item.price}}
        <button @click="remove(index)">取消</button>
      </li>
    </ul>
    <h3>一共点了{{count}}道菜,消费{{allPrice}}元</h3>
  </div>
</template>

<script>
import { computed, defineComponent, reactive, toRefs } from 'vue'

export default defineComponent({
  name: 'todoList',
  data() {
    return {}
  },

  setup() {
    const add = (num1, num2) => {
      const a1 = ('' + num1).split('.')[1]
        ? ('' + num1).split('.')[1].length
        : 0
      const a2 = ('' + num2).split('.')[1]
        ? ('' + num2).split('.')[1].length
        : 0
      const m = Math.pow(10, Math.max(a1, a2))
      return (num1 * m + num2 * m) / m
    }
    const state = reactive({
      list: [
        {
          name: '四喜丸子',
          price: 20.88,
        },
        {
          name: '狮子头',
          price: 30.88,
        },
        {
          name: '辣子鸡',
          price: 40.88,
        },
        {
          name: '糖醋鲤鱼',
          price: 50.88,
        },
      ],
      aList: [],

      count: computed(() => {
        return state.aList.length
      }),
      allPrice: computed(() => {
        let allPrice = 0
        state.aList.map((item) => {
          allPrice = add(allPrice, item.price)
        })
        return allPrice
      }),
      add(index) {
        console.log('你点的是', state.list[index])
        state.aList.push(state.list[index])
      },
      remove(index) {
        console.log('你取消了', state.aList[index])
        state.aList.splice(index, 1)
      },
    })
    return {
      ...toRefs(state),
    }
  },
})
</script>

<style lang="less" scoped>
</style>