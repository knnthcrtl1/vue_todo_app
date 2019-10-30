<template>
    <div class="todo__modal" @click="modalClose">
        <div class="todo__modal--inner--container">
            <p>Remove </p>
            <form v-on:submit.prevent="updateTodo(todoText)">
                <input 
                    type="text" 
                    class="input--todo" 
                    placeholder="add todo item" 
                    :value="modalTodo.text"
                    v-on:change="onChangeModal"
                />
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: 'todo__modal',
    data(){
        return {
            todoText: this.modalTodo.text
        }
    },
    props: {
        modalTodo: {
            type: Object
        }
    },
    methods: {
        modalClose: function (event) {
            this.$emit('modalClose', event)
        },
        updateTodo: function(todoText) {
            event.preventDefault();
            this.$emit('updateTodo', todoText, this.modalTodo.id)
        },
        onChangeModal: function(e) {
           this.todoText = e.target.value;
        }
    }
}
</script>

<style scoped>
.todo__modal {
    background-color: rgba(0,0,0,0.8);
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}

.todo__modal--inner--container {
    background-color: #fff;
    padding: 30px;
    width: 100%;
    margin: 0 auto;
    max-width: 420px;
    margin-top: 100px;
}
   .input--todo {
    width: 100%;
    max-width: 300px;
    padding: 10px 15px;
    box-shadow: 0px 0px 2px 2px rgba(0,0,0,0.3);
    border: none;
    border-radius: 12px;
    font-size: 16px;
}
</style>