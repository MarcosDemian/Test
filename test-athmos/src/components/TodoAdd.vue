<template>
    <div id="add-container">
        <form @submit="addTodo">
            <input type="text" v-model="title" placeholder="➕ Añadir">
        </form>
    </div>
</template>

<script>
import { uuid } from 'vue-uuid';

export default {
    name: 'TodoAdd',
    data(){
        return {
            title: ''
        }
    },
    methods:{
        addTodo(e){
            e.preventDefault();

            const newTodo = {
                id: uuid.v4(),
                title: this.title,
                completed: false
            };

            this.title = '';
            this.$emit('add-todo', newTodo);
        },
        updateLocalStorage:function(){
            localStorage.setItem('todos', JSON.stringify(this.addTodo))
        },
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Gulzar&display=swap');

    #add-container{
        padding: 0 10px 0 10px;
    }
    input{
        padding: 10px;
        outline: none;
        border: solid 1px #ccc;
        border-radius: 20px;
        width: 100%;
        background-color: #00c297;
    }

    input::placeholder{
        color: white;
        font-family: Gulzar, sans-serif;
    }
</style>