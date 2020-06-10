<template>
  <form v-on:submit.prevent="onSubmit">
    <input type="text" v-model="title" />
    <button class="but" type="submit">Create</button>
  </form>
</template>


<script>
export default {
  data() {
    return {
      title: ""
    };
  },

  methods: {
    onSubmit() {
      if (this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false
        };
        this.$emit("add-todo", newTodo);
        this.title = "";
      }
    }
  }
};
</script>



<style scoped>
form {
  display: flex;
}

input {
  width: 100%;
  border: 2px solid rgb(65, 168, 168);
  border-radius: 5px;
}

.but {
  margin: 0 10px 0 10px;
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