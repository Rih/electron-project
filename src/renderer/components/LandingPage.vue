<template>
  <div class="container">
      <div>
          <input type="text" 
          class="todo-input"
          v-model="todoItemName" 
          placeholder="What are you doing today?" 
          @keyup.enter.prevent="addTodo"
          >
      </div>

      <div class="todos">
        <ul>
          <li class="todo-item" 
          v-for="todo in todos" 
          :key="todo.id" 
          @click="completeTodo(todo)" 
          >{{ todo.name }}</li>
        </ul>
      </div>
  </div>  
</template>


<script>

import { mapState } from 'vuex';

export default {
    data(){
      return {
        todoItemName: ""
      }
    },
    methods: {
      addTodo(){
        this.$store.dispatch("ADD_TODO", this.todoItemName);
        this.todoItemName = "";
      },
      completeTodo(selectedTodo){
        this.$store.dispatch("COMPLETE_TODO", selectedTodo.id);
      }
    },
    computed: {
      ...mapState({
        todos: state => state.Todo.todos
      })
    }
}
</script>

<style>
  .container{
    height: 100vh;
    text-align: center;
    background: #30336b;
  }
  .todo-input {
    font-size: 36px;
    width: 90vw;
    border: 0px;
    outline: none;
    margin-top: 20px;
    text-align: center;
    background-color: transparent;
    color: white;
  }

  .todos {
    overflow: scroll;
    height: 70vh;
    margin-top: 10px;
  }

.todo-item {
  font-size: 24px;
  color: white;
  padding: 10p 0px;
}

::placeholder {
  color: rgba(255, 255, 255, 0.7);
}

</style>
