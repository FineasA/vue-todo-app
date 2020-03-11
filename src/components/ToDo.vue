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
            :class="{ active: task.isHovering }"
            @mouseover="hovering(index)"
            @mouseleave="notHovering(index)"
          >
            <input
              type="text"
              v-show="task.edit"
              :placeholder="task.todo"
              v-model="editPersonQuery"
              @keyup.enter="confirmEdit(index)"
            />
            <span
              class="task-item"
              @click="editTask(index)"
              v-show="!task.edit"
            >
              {{ task.todo }}
            </span>

            <button
              style="margin-left: 25px"
              class="btn btn-primary"
              :key="index"
              @click="deleteTask(index)"
            >
              Delete
            </button>
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
import config from "../config.js";

export default {
  data() {
    return {
      editPersonQuery: "",
      query: "",
      task: {},
      todos: []
    };
  },
  methods: {
    getUpdatedList() {
      this.$http.get(config.url).then(response => {
        console.log(response.data);
        this.todos = response.data;
      });
    },
    updateList() {
      this.$http.put(config.url, this.todos);
    },
    confirmEdit(index) {
      this.todos[index].todo = this.editPersonQuery;
      this.todos[index].edit = false;
      this.updateList();
      this.editPersonQuery = "";
    },
    editTask(index) {
      this.todos[index].edit = true;
    },
    deleteTask(index) {
      this.todos.splice(index, 1);
      this.updateList();
    },
    addTask() {
      this.task = {
        isCompleted: false,
        todo: this.query,
        isHovering: false,
        edit: false,
        date: new Date()
      };
      this.todos.push(this.task);
      //post request to update list
      this.updateList();
      this.query = "";
    },
    hovering(index) {
      this.todos[index].isHovering = true;
    },
    notHovering(index) {
      this.todos[index].isHovering = false;
    }
  },
  mounted() {
    console.log("mounted");
    this.getUpdatedList();
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

.task-item {
  cursor: text;
}
</style>
