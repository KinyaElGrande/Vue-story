<template>
  <div>
      <input type="text" class="todo-input" 
      placeholder="What needs to be done" v-model="newTodo" @keyup.enter="addTodo">
      <todo-item v-for="todo in todos" :key="todo.id" :todo="todo" :index="index"
       @removedTodo="removeTodo" @finishedEdit="finishedEdit" :checkAll="!anyRemaining">

      </todo-item>
      <div class="extra-container">
          <div><label><input type="checkbox" :checked="!anyRemaining"
          @change="checkallTodos">Check All</label></div>
          <div>{{ remaining}} items left </div> 
      </div>

      <div class="extra-container">
          <div>
              <button :class="{ active: filter == 'all'}" @click="filter = 'all'">All</button>
              <button :class="{ active: filter == 'active'}"
              @click="filter = 'active'">Active</button>
              <button :class="{ active: filter == 'completed'}"
              @click="filter = 'completd'">Completed</button>
          </div>

          <div>
              Clear Completed 
          </div>
      </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem'

export default { 
  name: 'todo-list',
  components: {
      TodoItem,
  },

  data () {
      return {
          newTodo: '',
          idForTodo: 4,
          beforeEditCache: '',
          filter: 'all',
          todos: [
              {
                  'id': 1,
                  'title': 'Exam week one',
                  'completed': true,
                  'editing' : false
              },
              {
                  'id': 1,
                  'title': 'Exam week two',
                  'completed': false,
                  'editing' : false
              },
              {
                  'id': 3,
                  'title': 'Thuguma week ',
                  'completed': false,
                  'editing' : false
              }
          ]
      }
  },
  computed: {
      remaining () {
          return this.todos.filter(todo => !todo.completed).length
      },
      anyRemaining () {
          return this.remaining != 0
      }
  },
  methods: {
      addTodo() {
          if(this.newTodo.trim().length == 0){
              return
          }
          this.todos.push({
              id: this.idForTodo,
              title: this.newTodo,
              completed: false
          })

          this.newTodo = ''
          this.idForTodo++
      },
      removeTodo(index) {
          this.todos.splice(index, 1)
      },
       checkallTodos() {
           this.todos.forEach((todo) => todo.completed = 
           event.target.checked)
       },
       finishedEdit(data) {
           this.todos.splice(data.index, 1, data.todo)
       }

  }
}
</script>

<!-- Add attribute to limit CSS to this component only -->
<style lang = "scss" >
    .todo-input{
        width: 100%;
        padding: 10px 18px;
        font-size: 18px;
        margin-bottom: 16px;

        &:focus {
            outline: 0;
        }
    }

    .todo-item {
        margin-bottom: 12px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    
    .remove-item {
        cursor: pointer;
        margin-left: 14px;
        &:hover {
            color: black;
        }
    }

    .todo-item-left {
        display: flex;
        align-items: center;
    }

    .todo-item-label {
        padding: 10px;
        border: 1px solid white;
        margin-left: 12px;
    }

    .todo-item-edit {
        font-size: 24px;
        color: #2c3e50;
        margin-left: 12px;
        width: 100%;
        padding: 10px;
        border: 1px solid #ccc;
        font-family: 'avenier', Arial, Helvetica, sans-serif;

        &:focus {
            outline: none;
        }
    }

    .completed {
        text-decoration: line-through;
        color: grey;
    }

    .extra-container{
        display: flex;
        align-items: center;
        justify-content: space-between;
        font-size: 16px;
        border-top: 1px solid lightgrey;
        padding-top: 14px;
        margin-bottom: 14px
    }
    button{
        font-size: 14px;
        background-color: white;
        appearance: none;

        &:hover {
            background: lightgreen;
        } 

        &:focus {
            outline: none;
        }
    }

    .active {
        background: lightgreen;
    }

</style>
