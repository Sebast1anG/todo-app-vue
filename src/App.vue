<template>
  <v-app>
    <v-main>
      <v-container>
        <TodoList />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList,
  },
}
</script>
