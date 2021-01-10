<template>
    <div class="todo-item">
        <div class="todo-item-label" v-if="!isEditing">
            <input type="checkbox"
                    :id="id"
                    :checked="isCompleted"
                    @change="$emit('checkbox-changed')"
            >
            <label :for="id">
                {{label}}
            </label>
        </div>
        <to-do-edit v-else :id="id" :label="label" @edit-save="itemSaved" @edit-cancel="editCancelled"></to-do-edit>
        <div class="todo-item-actions">
            <button class="btn" @click="toggleEditing">Edit</button>
            <button class="btn btn-delete" @click="deleteToDo">Delete</button>
        </div>
    </div>
</template>

<script>
import ToDoEdit from './ToDoEdit.vue'
export default {
  components: { ToDoEdit },
    name: 'ToDoItem',
    props: {
        label: {required: true, type: String},
        completed: {default: false, type: Boolean},
        id: {required: true, type: Number},
    },
    data() {
        return {
            isEditing: false
        }
    },
    methods: {
        deleteToDo() {
            this.$emit('item-deleted')
        },
        toggleEditing() {
            this.isEditing = !this.isEditing
        },
        itemSaved(newLabel) {
            this.$emit('item-saved', newLabel)
            this.isEditing = false
        },
        editCancelled() {
            this.isEditing = false
        }
    },
    computed: {
        isCompleted() {
            return this.completed
        }
    }
}
</script>

<style scoped>
    .todo-item {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: stretch;
    }
</style>