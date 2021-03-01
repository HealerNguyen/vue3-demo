<template>
  <h1>{{ msg }}</h1>
  <button @click="increment">
    Count is: {{ event.count }}, double is: {{ event.double }}
  </button>
</template>
<!-- ref use .value, reactive not .value -->
<script>
import { ref, toRefs, onMounted, watch, computed, reactive, watchEffect } from 'vue'
// import useSearch from '@use/search'
export default {
  name: 'About',
  setup() {
    const test = callTest()
    // const xSearch = useSearch()
    const xEvent = reactive({
      msg: 'About Page',
    })
    const event = reactive({
      // msg: 'About Page',
      count: 0,
      double: computed(() => event.count * 2)
    })
    function increment() {
      event.count++
    }
    // watch([event.msg,event.count], ([newMsg, newCount], [oldMsg, oldCount]) => {
    //   console.log('---')
    // })
    watchEffect(() => {
      console.log(event.count)
    })
    return {
      ...toRefs(xEvent),event,test,increment,
      // xSearch
    }
  }
}
// composition function
function callTest() {
  console.log('====')
}
</script>
