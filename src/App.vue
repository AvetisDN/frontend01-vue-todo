<template>
  <div id="app">
    <h1>To Do List</h1>
    <to-do-form @todo-added="addToDo"></to-do-form>
    <ul class="list">
      <li v-for="todo in todoList" :key="todo.id">
        <to-do-item 
          :label="todo.label" 
          :completed="todo.completed" 
          :id="todo.id" 
          @checkbox-changed="updateTodoList(todo.id)"
          @item-saved="editToDoItem(todo.id, $event)"
          @item-deleted="deleteToDoItem(todo.id)"
        >
        </to-do-item>
      </li>
    </ul>
    <p>
      {{summary}}
    </p>
  </div>
</template>

<script>
import ToDoForm from './components/ToDoForm.vue'

import ToDoItem from './components/ToDoItem'

export default {
  name: 'App',
  components: {
    ToDoItem,
    ToDoForm
  },
  data() {
    return {
      todoList: [
        {label: 'Learn HTML/CSS', completed: true, id: 1},
        {label: 'Learn basic JS', completed: true, id: 2},
        {label: 'Learn React', completed: true, id: 3},
        {label: 'Learn Vue', completed: false, id: 4},
        {label: 'Learn Angular', completed: false, id: 5},
      ]
    }
  },
  methods: {
    addToDo(label) {
      this.todoList.push({label: label, completed: false, id: this.todoList.length+1})
    },
    updateTodoList(id) {
      const itemToUpdate = this.todoList.find(item => item.id === id)
      itemToUpdate.completed = !itemToUpdate.completed
    },
    deleteToDoItem(id) {
      const itemToDelete = this.todoList.findIndex(item => item.id === id)
      this.todoList.splice(itemToDelete, 1)
    },
    editToDoItem(id, newLabel) {
      const itemToEdit = this.todoList.find(item => item.id === id)
      itemToEdit.label = newLabel
    },
  },
  computed: {
    summary() {
      const numberOfCompleted = this.todoList.filter(item => item.completed).length
      return `Completed ${numberOfCompleted} of ${this.todoList.length}`
    }
  }
}
</script>

<style>

*, *::before, *::after {
  box-sizing: border-box;
}
input:focus {
  box-shadow: rgba(21, 131, 175, 0.6) 0 0 10px;
}
body {
  background-color: #f0f1f2;
  font-family: sans-serif;
  font-size: 16px;
}
#app {
  max-width: 500px;
  background-color: #fff;
  box-shadow: rgba(0,0,0,.3) 0 5px 15px;
  padding: 2rem 1rem;
  border-radius: 5px;
  margin: 1rem auto;
  display: flex;
  flex-direction: column;
}
.list {
  list-style: none;
  margin: 1rem 0;
  padding: 0;
}
.list li {
  padding: .5rem;
  background-color: #f5f6f7;
  margin: .5rem 0;
}
.btn {
  border: none;
  border-radius: 4px;
  width: auto;
  padding: .5rem 1.5rem;
  background-color: #55666b;
  color: #fff;
  cursor: pointer;
  transition: 250ms ease;
  opacity: .8;
  border: 1px solid #55666b;
}
.btn:hover {
  opacity: 1;
}
input,textarea,button {
  font-family: inherit;
}
input {
  border: 1px solid #9ab;
  border-radius: 4px;
  width: auto;
  padding: .5rem;
  background-color: #ffffff;
  color: rgb(72, 76, 78);
  transition: 250ms ease;
  opacity: .8;
}
.btn-ok {
  background-color: #0c721d;
  border-color: #0c721d;
}
.btn-cancel {
  background-color: #c85d15;
  border-color: #c85d15;
}
.btn-delete {
  background-color: #921818;
  border-color: #921818;
}
</style>
