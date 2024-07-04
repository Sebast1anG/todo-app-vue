<template>
  <div>
    <v-text-field v-model="newTodo" @keyup.enter="addTodo" label="Add a todo"></v-text-field>
    <v-list>
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @remove="removeTodo"
        @update-done="toggleDone"
      />
    </v-list>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue'

export default {
  name: 'TodoList',
  components: {
    TodoItem,
  },
  data() {
    return {
      newTodo: '',
      todos: [],
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === '') return
      this.todos.push({
        id: Date.now(),
        text: this.newTodo.trim(),
        done: false,
      })
      this.newTodo = ''
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    toggleDone(id) {
      const todo = this.todos.find(todo => todo.id === id)
      if (todo) {
        todo.done = !todo.done
      }
    },
  },
}
</script>
