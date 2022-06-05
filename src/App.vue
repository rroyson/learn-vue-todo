<template>
  <h1>Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <input v-model="newTodo" name="New Todo" />
    <button>Add Todo</button>
  </form>
  <div v-for="(todo, index) in todos" :key="todo.id">
    <ul>
      <li class="todo">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
          {{ todo.content }}
        </h3>
        <button @click="removeTodo(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  setup() {
    const newTodo = ref('')
    const todos = ref([])

    function addNewTodo() {
      todos.value.push({ id: Date.now(), done: false, content: newTodo.value })
      newTodo.value = ''
    }

    function toggleDone(todo) {
      todo.done = !todo.done
    }

    function removeTodo(index) {
      todos.value.splice(index, 1)
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.done {
  text-decoration: line-through;
}

.todo {
  cursor: pointer;
}
</style>
