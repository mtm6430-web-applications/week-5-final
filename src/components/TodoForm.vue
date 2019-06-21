<template>
  <div>
    <slot name="label"></slot>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo" />
    </form>
    <slot name="desc"></slot>
    <br />
    <slot>Default slot, placeholder content</slot>
  </div>
</template>
<script>
export default {
  data() {
    return {
      newTodo: ""
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.length) {
        this.$emit("newTodo", this.newTodo);
        this.newTodo = "";
      }
    }
  }
};
</script>
<style scoped>
input {
  min-width: 200px;
  padding: 10px 20px;
  font-size: 1.5rem;
}
</style>
