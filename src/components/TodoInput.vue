<template>
        <input 
        type="text" 
        class="input--todo" 
        placeholder="add todo item" 
        :value="value" 
        v-on="listeners"/>
</template>

<script>
export default {
    name: 'todo__input',
    props:{
        value: {
            type: String,
            default: ''
        }
    },
    computed: {
        listeners() {
            return {
                ...this.$listeners,
                input: event => this.$emit('input', event.target.value)
            }
        }
    }
}
</script>

<style scoped>
    .input--todo[data-v-2fff0124] {
    width: 100%;
    max-width: 420px;
    padding: 10px 15px;
    box-shadow: 0px 0px 2px 2px rgba(0,0,0,0.3);
    border: none;
    border-radius: 12px;
    font-size: 16px;
}
</style>