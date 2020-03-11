<template>
  <div>
    <div class="row justify-content-center">
      <input
        type="text"
        placeholder="Enter task..."
        v-model="query"
        @keyup.enter="addTask"
      />
    </div>
    <br />
    <div class="row justify-content-center">
      <ul class="list-group">
        <transition-group
          enter-active-class="animated rollIn"
          leave-active-class="animated bounceOut"
        >
          <li
            class="list-group-item"
            v-for="(task, index) in todos"
            :key="index"
            @click="deleteTask(index)"
          >
            {{ task.todo }}
          </li>
        </transition-group>
      </ul>
    </div>
    <br />
    <div class="row justify-content-center">
      <div class="btn btn-primary" @click="addTask">Add Task</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: "",
      task: {},
      todos: []
    };
  },
  methods: {
    deleteTask(index) {
      this.todos.splice(index, 1);
    },
    addTask() {
      this.task = {
        isCompleted: false,
        todo: this.query
      };
      this.todos.push(this.task);
      this.query = "";
    }
  }
};
</script>

<style>
.list-group-item {
  cursor: pointer;
}
</style>
