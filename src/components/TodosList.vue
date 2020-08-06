<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import Header from "../components/layout/Header";
import AddTodo from "../components/AddTodo"
import axios from "axios";
const baseURI = "https://jsonplaceholder.typicode.com/todos";

export default {
  name: "TodosList",
  components: {
    Todos,
    Header,
    AddTodo,
  },
  data() {
    return {
      msg: "Hello Flora",
      todos: [],
      // {
      //   id:1,
      //   title:'todo one',
      //   completed:true
      // },
      //  {
      //   id:2,
      //   title:'todo two',
      //   completed:false
      // },
      //  {
      //   id:3,
      //   title:'todo three',
      //   completed:false
      // }
    };
  },
  created() {
    this.getTodos();
  },
  mounted() {
    // if you want to call it on component mounted
    this.getTodos();
  },
  methods: {
    deleteTodo(id) {
       axios
        .delete(baseURI+"/"+id)
        .then((res) => {
         this.todos = this.todos.filter((todo) => todo.id !== id);
          console.log(res);
        })
        .catch((err) => {
          console.log(err);
        });
       
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios
        .post(baseURI, { title, completed })
        .then((res) => {
          this.todos = [...this.todos, res.data];
        })
        .catch((err) => {
          console.log(err);
        });
    },
    getTodos() {
      axios
        .get(baseURI + "?_limit=5")
        .then((res) => (this.todos = res.data))
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
  width: 50rem;
  margin: 0 auto;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
