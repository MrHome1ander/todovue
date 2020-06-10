<template>
  <li>
    <span v-bind:class="{done:todo.completed}">
      <input type="checkbox" v-on:change="todo.completed = !todo.completed" />
      <strong>{{index+1 }}</strong>
      {{todo.title | upperCase}}
    </span>
    <button class="rm" v-on:click="$emit('remove-todo',todo.id)">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    upperCase(value) {
      return value.toUpperCase();
    }
  }
};
</script>

<style scoped>
li {
  border: 2px solid #ccc;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 2rem;
  margin-bottom: 1rem;
}

.rm {
  background: rgb(65, 168, 168);
  border: none;
  color: #fff;
  border-radius: 5px;
  font-size: 20px;
  font-weight: bold;
}

.rm:hover {
  background: red;
  transition: ease-out 0.3s;
}

input {
  margin-right: 1rem;
}

.done {
  text-decoration: line-through;
}
</style>