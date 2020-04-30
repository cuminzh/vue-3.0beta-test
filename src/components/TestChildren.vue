<template>
  <div>{{num}}</div>
  <div>{{nums}}</div>
  <button @click="add">add</button>
  <div>{{foo}}</div>
  <div>{{bar}}</div>
</template>

<script>
  import { watch, ref, computed, reactive, toRefs } from 'vue'

  export default {
    name: 'TestChildren',
    props: {
      childCount: Number
    },
    setup (props) {
      const num = ref(1)
      // let nums = computed(() => num.value + 1)
      let nums = ref(0)
      const add = () => {
        num.value++
        // nums.value = 0
      }
      watch(num, () => {
        nums.value += 3
      })
      const {foo, bar} = useFeatureX()
      return {
        num,
        nums,
        add,
        foo,
        bar,
      }
    },
  }
  function useFeatureX() {
    const states = reactive({
      foo: 1,
      bar: 2
    })
    return toRefs(states)
  }
</script>

<style scoped>

</style>
