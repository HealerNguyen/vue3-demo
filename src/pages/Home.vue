<template>
  <h1>{{ msg }}</h1>
  <button @click="count++">count is: {{ count }}</button>
  <button @click="getTodos()">Fetch todos</button>
  <h4>Todos List completed</h4>
  <ul>
    <li v-for="(todo, index) in filterCompleteds" :key="index">{{todo.title}} --- {{todo.completed ? '(completed)' : '(inprogress)'}}</li>
  </ul>
  <h4>Todos List</h4>
  <ol>
    <li @click="markCompleted(index)" v-for="(todo, index) in todos" :key="index">{{todo.title}} --- {{todo.completed ? '(completed)' : '(inprogress)'}}</li>
  </ol>
</template>

<script>
import { ref, onMounted, watch, computed } from 'vue'
export default {
  name: 'HelloWorld',
  setup(props) {
    const count = ref(0)
    const msg = ref('Home Page')
    const todos = ref([])
    const getTodos = () => {
      todos.value = [
        {
          "userId": 1,
          "id": 1,
          "title": "delectus aut autem",
          "completed": false
        },
        {
          "userId": 1,
          "id": 2,
          "title": "quis ut nam facilis et officia qui",
          "completed": false
        },
        {
          "userId": 1,
          "id": 3,
          "title": "fugiat veniam minus",
          "completed": false
        },
        {
          "userId": 1,
          "id": 4,
          "title": "et porro tempora",
          "completed": true
        },
        {
          "userId": 1,
          "id": 5,
          "title": "laboriosam mollitia et enim quasi adipisci quia provident illum",
          "completed": false
        },
      ]
      console.log(todos.value)
    }
    const markCompleted = (index) => {
      let status = todos.value.find((el, i) => i === index).completed
      todos.value.find((el, i) => i === index).completed = !status
    }
    onMounted(() => {
      getTodos()
      console.log('Component is mounted!')
    })
    const filterCompleteds = computed(() => {
      return todos.value.filter(el => el.completed == true)
      console.log('tra ve gia tri khi todos thay doi')
    })
    watch(count, (newValue, oldValue) => {
      console.log('The new count value is: ' + count.value)
    })
    return {
      msg,
      count,
      todos,
      getTodos,
      markCompleted,
      filterCompleteds
    }
  }
}
</script>
