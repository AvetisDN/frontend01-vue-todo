<template>
    <form @submit.prevent="onSubmit">
        <label for="new-todo-item">
            Things to do
        </label>
        <input type="text" 
            id="new-todo-item" 
            name="new-todo" 
            autocomplete="off"
            v-model.trim="label"
        >
        <button type="submit" class="btn btn-ok">
            Add
        </button>
        <p class="error-message" v-if="error">Fill the label field</p>
    </form>
</template>

<script>
export default {
    name: 'ToDoForm',
    data() {
        return {
            label: '',
            error: false
        }
    },
    methods: {
        onSubmit() {
            if(this.label === '') {
                this.error = true
                return
            }
            this.$emit('todo-added', this.label)
            this.error = false
            this.label=''
        }
    }
}
</script>