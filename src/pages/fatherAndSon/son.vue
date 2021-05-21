<template>
  <div>{{propCotent}}</div>
</template>

<script>
import {watch} from 'vue'
import { watchEffect } from 'vue'
export default {
  name: 'son',
  props: {
    name: String,
  },
  data() {
    return {}
  },
  setup(props,context) {
    let propCotent
    watchEffect(() => {
      propCotent = props.name
    })
    watch(() =>props.name,(newName,oldName) =>{
      console.log(newName,oldName)
      context.emit('name-changed')  // 相当于 this.$emit

    })
    return {
      propCotent,
    }
  },
}
</script>

<style lang="less" scoped>
</style>