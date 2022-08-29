<template>
  <div id="app" class="container">
    <h1 class="text-center">todo app</h1>
    <input 
      type="text" 
      class="w-100 p-2" 
      placeholder="Type todo"
      @keyup.enter="addTodo"
      v-model="todoText"
    >
    <hr>
    <Todocomponent
  
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle-checkbox="toggleCheckbox"
      @click-delete="clickDelete"
      />




  </div>
</template>

<script>

import Todocomponent from '@/components/Todocomponent.vue';



export default {
    components: { 
      Todocomponent 
    },
    data() {
      return{
        todoText: '',
        todos: [
          {id: 1, text: 'buy a car',checked:false},
          {id:2, text: 'play a game',checked:false},
        ]
      }
    },
    methods: {
      addTodo(e) {
          this.todos.push({
            id: Math.random(),
            text: e.target.value,
            checked: false
          });
          this.todoText='';

      },
      toggleCheckbox({id,checked}){
        const index = this.todos.findIndex(todo => {
          return todo.id === id;

        });
        this.todos[index].checked = checked;

      },
      clickDelete(id){
        const index = this.todos.findIndex(todo => {
          return todo.id === id;

        });
        this.todos.splice(index,1);
        

      }
    }

}

</script>

<style>

</style>
