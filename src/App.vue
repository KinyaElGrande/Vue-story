<template>
  <div id="app">
    <Todos v-bind:todos="Todos" />
  </div>
</template>

<script>
import Todos from './components/Todos';

export default {
  el: "#app",
  components: {
    Todos
  },
  data(){
    return{
      todos: [
        {
          id: 1,
          title: "Exam week 1",
          completed: false
        },
        {
          id: 2,
          title: "Exam week 2",
          completed: true
        },
        {
          id: 3,
          title: "Back to coding hehe",
          completed: false
        }
      ]
    }
  }
}
</script>

<style>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>