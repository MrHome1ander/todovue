<template>
  <div>
    <h2>Home page</h2>

    <p>Here is simple ToDo app on Vue JS!</p>
    <router-link class="but" to="/todovue/todos">Todos</router-link>
  </div>
</template>


<style scoped>
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