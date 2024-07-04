<template>
  <v-list-item>
    <v-list-item-action>
      <v-checkbox v-model="localTodo.done" @change="toggleDone"></v-checkbox>
    </v-list-item-action>
    <v-list-item-content>
      <v-list-item-title :class="{ done: localTodo.done }">{{ localTodo.text }}</v-list-item-title>
    </v-list-item-content>
    <v-list-item-action>
      <v-btn icon @click="$emit('remove', localTodo.id)">
        <v-icon>mdi-delete</v-icon>
      </v-btn>
    </v-list-item-action>
  </v-list-item>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: Object,
  },
  data() {
    return {
      localTodo: { ...this.todo },
    }
  },
  methods: {
    toggleDone() {
      this.$emit('update-done', this.localTodo.id)
    },
  },
}
</script>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
