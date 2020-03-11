<template>
  <div>
    <div class="row justify-content-center">
      <input
        class="input"
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
            :class="{ active: task.isHovering }"
            @mouseover="hovering(index)"
            @mouseleave="notHovering(index)"
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
        todo: this.query,
        isHovering: false
      };
      this.todos.push(this.task);
      this.query = "";
    },
    hovering(index) {
      this.todos[index].isHovering = true;
    },
    notHovering(index) {
      this.todos[index].isHovering = false;
    }
  }
};
</script>

<style>
.list-group-item,
.btn {
  cursor: pointer;
  font-family: "Baloo Chettan 2", cursive;
}

.input {
  font-family: "Baloo Chettan 2", cursive;
}
</style>
