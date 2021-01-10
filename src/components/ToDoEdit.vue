<template>
    <div class="todo-item-label">
        <form @submit.prevent="onSubmit">
            <div class="form-control">
                <label :for="id">Edit label</label>
                <input type="text" :id="id" autocomplete="off" v-model.trim="newLabel">
            </div>
            <div class="btn-group">
                <button type="button" class="btn btn-cancel" @click="onCancel">Cancel</button>
                <button type="submit" class="btn btn-ok">Save</button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: 'ToDoEdit',
    props: {
        label: {required: true, type: String},
        id: {required: true, type: Number},
    },
    data() {
        return {
            newLabel: this.label
        }
    },
    methods: {
        onSubmit() {
            if(this.newLabel && this.newLabel !== this.label) {
                this.$emit('edit-save', this.newLabel)
            }
        },
        onCancel() {
            this.$emit('edit-cancel')
        }
    }
}
</script>