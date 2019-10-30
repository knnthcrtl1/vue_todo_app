<template>
    <div id="todo__list">
        <ul>
            <TodoListItem 
                v-for="todo in todos"
                :key="todo.id"
                :todo="todo"
                @modalOpen="modalOpen"
                @removeTodo="removeTodo"
            />
            <!-- <TodoListItem 
                v-for="todo in todos"
                :key="todo.id"
                :todo="todo"
                @remove="remove"
                @modalOpen="modalOpen"
            /> -->
        </ul>
    </div>
</template>

<script>
import TodoListItem from './TodoListItem.vue';

export default {
    name: 'todo__itodo__listnput',
   props: {
       todos: {
           type: Array
       },
       modalValue:{
           type: Boolean
       }
   },
    components:{
        TodoListItem    
    },
    methods: {
       removeTodo: function(id) {
           this.$emit('removeTodo', id);
       },
       modalOpen: function(todoText) {
           this.$emit('modalOpen', todoText);
       }
    }
}
</script>

<style scoped>
div#todo__list {
    width: 420px;
    margin: 0 auto;
    text-align: left;
}
div#todo__list ul {
    margin: 0;
    padding: 0;
    margin-top: 20px;
}
div#todo__list ul li{
    list-style: none;
    cursor: pointer;
    padding: 10px;
}

div#todo__list ul li:nth-child(odd){
    background-color: #cccccc;
}

div#todo__list ul li:nth-child(even){
    background-color: #f2f2f2;
}

</style>