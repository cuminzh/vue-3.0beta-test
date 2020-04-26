<template>
  <div class="div-test">{{count}} {{object.foo}}</div>
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
      const object = reactive({ foo: 'bar' })
      // return () => h('div', [count.value, object.foo])
      return {
        count,
        object
      }
    }
  }
</script>

<style scoped>

</style>
