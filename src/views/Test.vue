<template>
  <div class="div-test">{{count}} {{object.foo}}</div>
  <div>{{countString}}</div>
  <test-children :child-count="count"/>
</template>

<script>
  import {h, ref, reactive } from 'vue';
  import TestChildren from '../components/TestChildren'

  export default {
    name: 'Test',
    components: {TestChildren},
    setup () {
      const count = ref(0)
      const countString = ref('dd')
      const object = reactive({ foo: 'bar' })
      // return () => h('div', [count.value, object.foo])
      return {
        count,
        object,
        countString
      }
    }
  }
</script>

<style scoped>

</style>
