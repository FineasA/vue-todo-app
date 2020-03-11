<template>
  <div class="container">
    <div class="row justify-content-center">
      <h2 class="title">Task Manager</h2>
    </div>
    <hr />
    <to-do></to-do>
  </div>
</template>

<script>
import ToDo from "./components/ToDo.vue";

export default {
  components: {
    ToDo
  }
};
</script>

<style>
.title {
  font-family: "Roboto Condensed", sans-serif;
}
</style>
