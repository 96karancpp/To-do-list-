<template>
<div id="app">
  <h1>To do App</h1>
  <input type="text" v-model="todoName" @keyup.enter="addTodo">
  <div>
    <ul>
      <li v-for="todo of todos" v-bind:key = "todo.id">{{todo.name}}<button>Delete</button></li>
    </ul>
  </div>
  </div>

</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
const baseURL = "http://localhost:3000/todos";

Vue.use(VueAxios, axios)


export default {
  name: 'App',
  data(){
    return{
      todos:[],
      todoName:""
    }
  },
  async created(){
    try{
      const res = await axios.get(baseURL);
      this.todos = res.data;
    }catch(e){
      console.error(e);
    }
  },
  methods:
  {
    async addTodo()
    {
      const res = await axios.post(baseURL,{name:this.todoName});
      this.todos = [...this.todos,res.data];
      this.todoName = "";
    }
  }
}
</script>

<style>
*{
  margin: 0px;
  padding: 0px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #042e58;
  margin-top: 10px;
}
#app img{
  height: 100px;
  width: 100px;
}


</style>
