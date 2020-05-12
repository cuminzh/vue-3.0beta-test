<template>
  <div>{{num}}</div>
  <div>{{nums}}</div>
  <button @click="add">add</button>
  <div>{{foo}}</div>
  <div>{{bar}}</div>
  <div>x:{{x}}, y:{{y}}</div>
</template>

<script>
  import { watch, ref, computed, reactive, toRefs, onMounted } from 'vue'
  import useMouse from '../utils/listenMouse'

  export default {
    name: 'TestChildren',
    props: {
      childCount: Number
    },
    setup (props) {
      const num = ref(1)
      // let nums = computed(() => num.value + 1)
      let nums = ref(0)
      let { x, y } = useMouse()
      const add = debounce(()=>{
        num.value++
      }, 2000)
      watch(num, () => {
        nums.value += 3
      })
      const { foo, bar } = useFeatureX()
      onMounted(()=>{
        // document.addEventListener('click', debounce(()=>{
        //   console.log('防抖')
        // }, 200), true)

        document.addEventListener('scroll', throttle(()=>{
          console.log('节流')
        },200), true)
      })
      return {
        num,
        nums,
        add,
        foo,
        bar,
        x,
        y
      }
    },
  }

  function useFeatureX () {
    const states = reactive({
      foo: 1,
      bar: 2
    })
    return toRefs(states)
  }

  //防抖
  function debounce (fn, delay) {
    let timer
    return function () {
      if (timer) {
        clearTimeout(timer)
      }
      timer = setTimeout(() => {
        fn()
      }, delay)
    }
  }

  //节流
  function throttle (fn, delay) {
    let flag = ref(true)
    return () => {
      if (!flag.value) return
      flag.value = false
      setTimeout(() => {
        fn()
        flag.value = true
      }, delay)
    }
  }
</script>

<style scoped>

</style>
