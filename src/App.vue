<template>
  <div>
    <div id="header">
      <div class="logo-container">
        <img class="logo" src="./assets/logo1.png">
      </div>

      <ul>
        <li>➀ Estado de tareas</li>
        <li>➁ Estado de cuenta</li>
        <li>➂ Detalles de estado</li>
        <li>➃ Distribución</li>
        <li>➄ Cierres</li>
      </ul>
    </div>

    <div class="title-container">
      <img class="image" src="./assets/hombre.png" >
      <div class="text-container">
        <h5>Estado de tareas</h5>
        <p>Guia estado de tareas ˅</p>
      </div>
    </div>

    <div id="main-container">
      <TodoAdd v-on:add-todo="addTodo"/>
      <Search v-on:query-change="querySearch" />
      <Todos v-bind:todoslist="copyTodos" v-on:delete-todo="deleteTodo" />
    </div>
  </div>
</template>

<script>
import Search from './components/Search';
import Todos from './components/Todos';
import TodoAdd from './components/TodoAdd';

export default {
  name: 'App',
  components: {
    Todos, TodoAdd, Search
  },
  methods: {
    deleteTodo(id){
      this.todos = this.todos.filter(todo => todo.id != id);
      this.copyTodos = [...this.todos];
    },
    addTodo(todo){
      this.todos.push(todo);
      localStorage.setItem("tareas", JSON.stringify(this.todos));
      this.copyTodos = [...this.todos];
    },
    querySearch(query){
      if(query.trim() === ''){
        this.copyTodos = [...this.todos];
      }else{
        const temp = this.todos.filter(todo =>{
          return todo.title.includes(query)
        });

        this.copyTodos = [...temp];
      }
    }
  },
  created(){
    let data = localStorage.getItem("tareas")
    if(data != null){
      this.tareas = JSON.parse(data)
    }
  },

  data(){
    return {
      todos: [
        {
          id: 0,
          title:  'Comienza a añadir tareas',
          completed: false
        }
      ],
      copyTodos: []
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Gulzar&display=swap');

  *{
    box-sizing: border-box;
  }

  body{
    font-family: Gulzar, sans-serif;
    font-size: 1.5em;
    padding: 0;
    margin: 0;
  }

  #main-container{
    border: none;
    border-radius: 5px;
    width: 600px;
    margin: 0 auto;
    box-shadow: 0px 0px 5px 1px rgba(31,31,31,0.27);
    -webkit-box-shadow: 0px 0px 5px 1px rgba(31,31,31,0.27);
    -moz-box-shadow: 0px 0px 5px 1px rgba(31,31,31,0.27);
  }

  #header{
    width: 100vw;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    background: white;
    padding: 5px;
    box-shadow: 0px 1px 5px -1px rgba(18, 18, 18, 0.450);
    -webkit-box-shadow: 0px 1px 5px -1px rgba(18, 18, 18, 0.450);
    -moz-box-shadow: 0px 1px 5px -1px rgba(18, 18, 18, 0.450);
  }

  ul{
    list-style-type: none;
    margin: 0;
    text-align: center;
    display: inline;
  }

  li{
  position: relative;
  font-size: 20px;
  float: left;
  text-align: center;
  margin: 0 15px;
  cursor: pointer;
  color: #717791;
  }

  li::before{
  content: "";
  position: absolute;
  width: 100%;
  height: 4px;
  border-radius: 4px;
  background-color: #00c297;
  bottom: -5px;
  left: 0;
  transform-origin: right;
  transform: scaleX(0);
  transition: transform 0.3s ease-in-out;
}

li:hover::before {
  transform-origin: left;
  transform: scaleX(1);
  }

h2{
  padding: 0 10px;
  text-align: center;
}

.logo{
  width: 100%;
  height: 100%;
}

.logo-container{
  display: flex;
  align-items: center;
  width: 10%;
}

.title-container{
  margin: 20px 0;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 20vh;
}

.image{
  height: 100%;
}

.text-container{
  margin: 0 20px;
  align-items: center;
}

h5{
  color: #1d2730;
  margin: 0;
}

p{
  color: #00c297;
  font-size: small;
  margin: 0;
}
</style>
