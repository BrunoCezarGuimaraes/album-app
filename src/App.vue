<template>
  <h1 class="h">Header</h1>
  <router-view></router-view>
  <h1 class="h">Footer</h1>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: lightgrey;
  border-radius: 1rem;
}
.h {
  padding: 10px;
}
</style>
