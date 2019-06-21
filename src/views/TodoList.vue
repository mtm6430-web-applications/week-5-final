<template>
  <div>
    <h1>Todo List</h1>
    <TodoForm @newTodo="addTodo" />
    <Todo :todos="todoList" @removeTodo="appDeleteTodo" />
  </div>
</template>
<script>
import Todo from "@/components/Todo.vue";
import TodoForm from "@/components/TodoForm.vue";

// We will simply need to import axios since it a node package we do not need to specify a file.
import axios from "axios";

export default {
  components: {
    Todo,
    TodoForm
  },
  data() {
    return {
      todoList: []
    };
  },
  methods: {
    appDeleteTodo(index) {
      this.todoList.splice(index, 1);
      axios.put(
        "https://vue-and-axios.firebaseio.com/data.json",
        this.todoList
      );
    },
    addTodo(todo) {
      this.todoList.push(todo);

      // Making an axios put request to send the todoList array to Firebase
      axios
        .put("https://vue-and-axios.firebaseio.com/data.json", this.todoList)
        .then(response => {
          // we are logging the status message on success
          console.log("Your data was saved status: " + response.status);
        })
        .catch(error => {
          // we are logging the error message
          console.log("There was an error in saving data: " + error.response);
        });
    }
  },
  // created is a life cycle hook which will run when the instance is created
  created() {
    // here we are making a GET request using AXIOS to get the data
    axios
      .get("https://vue-and-axios.firebaseio.com/data.json")
      .then(response => {
        // console.log(response);
        // console.log(response.data);

        // Checking if the response has some data
        if (response.data) {
          this.todoList = response.data;
        }
      })
      .catch(error => {
        console.log("There was an error in getting data: " + error.response);
      });
  }
};
</script>
<style>
ul {
  list-style: none;
  width: 50%;
  margin: 0 auto;
}
ul li {
  border-bottom: 1px solid #acacac;
  padding: 10px 0;
  margin-bottom: 10px;
}
</style>
