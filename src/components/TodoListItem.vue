<template>
    <!-- <li @click="$emit('remove', todo.id)">
        {{todo.text}}
    </li> -->
    <li class="todo__list--item" >
        <div @click="$emit('modalOpen', todo)">
            <span>{{todo.text}}</span>
        </div>
        <div v-on:click="removeTodo(todo.id)">
            <span>X</span>
        </div>
    </li>
</template>

<script>
export default {
    props: {
        todo: Object
    },
    methods: {
        removeTodo: function(id){
            this.$emit('removeTodo', id);
        }
    }
}
</script>

<style scoped>
    .todo__list--item{
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>