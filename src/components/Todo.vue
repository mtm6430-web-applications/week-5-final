<template>
  <ul>
    <li v-for="(todo, index) in todos" :key="index" @click="todoDone(index)">
      {{ todo }}
    </li>
  </ul>
</template>
<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true
    }
  },
  methods: {
    todoDone(index) {
      console.log(index);
      this.$emit("removeTodo", index);
    }
  }
};
</script>
