<template>
  <v-list-item>
    <v-row align="center" no-gutters>
      <v-col cols="auto" class="checkbox-column">
        <v-checkbox v-model="localTodo.done" @change="toggleDone"></v-checkbox>
      </v-col>
      <v-col cols="auto" class="flex-grow-1">
        <v-list-item-title :class="{ done: localTodo.done }">{{ localTodo.text }}</v-list-item-title>
      </v-col>
      <v-col cols="auto">
        <v-btn icon @click="$emit('remove', localTodo.id)">
          <v-icon>mdi-delete</v-icon>
        </v-btn>
      </v-col>
    </v-row>
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
