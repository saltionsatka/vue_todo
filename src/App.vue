<template>
    <div id="app">
        <Header />
        <addTodo @add-todo="addTodo"/>
        <todos :todos="todos" @del-todo="deleteTodo"></todos>
  </div>
</template>

<script>
import Todos from './components/Todos';
import Header from './components/layout/Header';
import AddTodo from './components/AddTodo';

const axios = require('axios').default;


export default {
  name: 'App',
  components: {
      Todos, Header, AddTodo
  },
  data(){
    return {
      todos: []
    }
  },
    methods: {
        deleteTodo(id) {
            axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
            .then(() => this.todos = this.todos.filter(todo => todo.id !== id))
            .catch(error => console.log(error));

        },
        addTodo(newTodo) {
            let { title, completed } = newTodo;
            axios.post('https://jsonplaceholder.typicode.com/todos', {
                title,
                completed
            })
            .then(response => this.todos = [...this.todos, response.data])
            .catch(error => console.log(error));
            this.todos = [...this.todos, newTodo];
            // Copies the current todos and adds the newTodo
        },
        mounted() {
            axios.get('https://jsonplaceholder.typicode.com/todos')
                .then(response => this.todos = response.data)
                .catch(error => console.log(error));
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
    .btn {
        display: inline-block;
        border: none;
        background: #555;
        color: #fff;
        padding: 7px 20px;
        cursor: pointer;
    }
    .btn:hover{
        background: #666;
    }
</style>
