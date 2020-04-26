<template>
  <div>{{num}}</div>
  <div>{{nums}}</div>
  <button @click="add">add</button>
</template>

<script>
  import { watch, ref, computed } from 'vue'

  export default {
    name: 'TestChildren',
    props: {
      childCount: Number
    },
    setup (props) {
      const num = ref(props.childCount + 1)
      let nums = computed(() => num.value + 1)
      const add = () => {
        num.value++
      }
      watch(num, val => {
        console.log(val)
        // nums = 3
      })
      return {
        num,
        nums,
        add
      }
    }
  }
</script>

<style scoped>

</style>
