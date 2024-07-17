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
import axios from 'axios'
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
    async fetchTodos() {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/todos')
        this.todos = response.data.slice(0, 10).map(todo => ({
          id: todo.id,
          text: todo.title,
          done: todo.completed,
        }))
      } catch (error) {
        console.error('Failed to fetch todos:', error)
      }
    },
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
  mounted() {
    this.fetchTodos()
  }
}
</script>
