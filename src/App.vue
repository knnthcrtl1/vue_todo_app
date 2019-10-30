<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <TodoInput 
        v-model="todoText"
        @keydown.enter="addTodo"/>
        <TodoList 
        :todos="todos"
        @removeTodo="removeTodo"
        @modalOpen="modalOpen"
        :modalValue="modalShow"
        />
         <!-- <TodoList 
        :todos="todos"
        @remove="removeTodo"
        @modalOpen="modalList"
        :modalValue="modalShow"
        /> -->
        <Modal 
          v-if="modalShow"
          @modalClose="modalClose"
          :modalTodo="modalTodo"
          @updateTodo="updateTodo"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import Modal from './components/ModalComponent/Modal.vue';
import axios from 'axios';


export default {
  name: 'app',
   components: {
    TodoInput,
    TodoList,
    Modal
  },
  data (){
    return {
      todoText: '',
      todos: [],
      post: [],
      result: null,
      modalShow: false,
      modalTodo: null
    }
  },
  methods:{
    addTodo: function () {
      if(this.todoText){
        this.todos.push({
          id: Date.now(),
          text: this.todoText
        })
        this.todoText = "";
      }
    },
    updateTodo: function (text, id) {
      
      this.todos = this.todos.filter(todo => {
          if (todo.id === id) {
            todo.text = text;
          }
        return todo;
        })

    this.modalShow = false;
    },
    removeTodo: function(id) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== id;
      })
    },
    modalOpen: function (modalTodo) {
      this.modalTodo = modalTodo;
      this.modalShow = true;
    },
    modalClose: function (e) {
      let targetClose = e.target.className;
      if (targetClose === 'todo__modal') this.modalShow = false;
    },
    fetchData: async function() {
      try {
        let result = await axios.get('https://jsonplaceholder.typicode.com/posts/');
        JSON.stringify(result);
        this.result = 'loading'
        if(result) {
          this.result = result;
        }
      } catch (error) {
        this.result = error
      }
    }
  },
  async mounted () {
    await this.fetchData();
}
}


</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

*, *:before, *:after{
  box-sizing: border;
}

.container{
  max-width: 1024px;
  margin: 0 auto;
  width: 100%;
}

.row{
  margin-left: 15px;
  margin-right: 15px;
}
</style>
