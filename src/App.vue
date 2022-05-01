<template>
  <main>
    <header>
      <h1>myTodo</h1>
      <p>Questa semplice todo app è stata realizzata con Vue.</p>
      <section id="todo-list-container">
        <ul id="todo-list">
          <li 
            v-for="(todo, index) in todoList" 
            :key="todo.id" 
            :data-index="index" 
            class="todo-item">
            <input @click="completedTodo()" type="checkbox">
            <input :class="'todo-item-input-' + index" type="text" @change="updateTodo(index)" :value="todo">
            <button @click="deleteTodo(index)">Delete</button>
          </li>
        </ul>
        <ul>
          <li>
            <input type="text" @change="addTodo(index)" placeholder="Aggiungi qualcosa alla lista" v-model="newTodo">
          </li>
        </ul>
      </section>
    </header>
  </main>
</template>

<script>

import TodoItem from './components/TodoItem.vue'

export default {
  name: 'App',
  components: {
    TodoItem,
  },
  data(){
    return{
      newTodo: '',
      todoList: [
        'fare la spesa',
        'portare fuori il cane'
      ]
    }
  },
  methods: {
    addTodo(){
      this.todoList.push(this.newTodo);
      this.newTodo = ''
    },
    updateTodo(index){
      let element = '.todo-item-input-' + index;
      let value = document.querySelector(element).value;
      this.todoList[index] = value;
    },
    deleteTodo(index){
      this.todoList.splice(index, index + 1)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
ul{
  margin: 0;
  padding: 0;
}
li{
  list-style: none;
  border-bottom: 1px solid grey;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
input{
  width: 100%;
  padding: .5rem 1rem;
  box-sizing: border-box;
  display: inline;
  border: none;
}
</style>
