<template>
  <div>
    <router-link class="but" to="/">Home</router-link>
    <hr />
    <AddTodo v-on:add-todo="addTodo"></AddTodo>
    <select class="custom-select" v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <hr />
    <Loader v-if="loading"></Loader>
    <TodoList v-else-if="filteredTodos" v-bind:todos="filteredTodos" v-on:remove-todo="removeTodo"></TodoList>
    <p v-else>Nothing ToDo!</p>
  </div>
</template>



<script>
import TodoList from "@/components/TodoList";
import AddTodo from "@/components/AddTodo";
import Loader from "@/components/Loader";
export default {
  name: "App",
  data() {
    return {
      todos: [],
      loading: false,
      filter: "all"
    };
  },
  mounted() {
    /*  fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then(response => response.json())
      .then(json => {
        this.todos = json;
        this.loading = false;
      }); */

    if (localStorage.getItem("todos"))
      this.todos = JSON.parse(localStorage.getItem("todos"));
  },
  watch: {
    todos: {
      handler() {
        console.log("Todos changed!");
        localStorage.setItem("todos", JSON.stringify(this.todos));
      },
      deep: true
    }
  },

  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      }

      if (this.filter === "completed") {
        return this.todos.filter(t => t.completed);
      }

      if (this.filter === "not-completed") {
        return this.todos.filter(t => !t.completed);
      }
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  }
};
</script>

<style scoped>
select {
  margin: 10px 0px;
}

.but {
  color: white;
  font-size: 20px;
  font-weight: bold;
  background: rgb(65, 168, 168);
  border: solid #2c3e50 1px;
  border-radius: 7px;
  padding: 5px;
  text-decoration: none;
}

.but:hover {
  background: #2c3e50;
  transition: ease-out 0.3s;
}
</style>