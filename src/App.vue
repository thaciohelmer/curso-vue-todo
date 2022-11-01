<template>
  <div id="app" class="container d-flex flex-column">
    <div class="row my-5">
      <div class="col-12">
        <h1 class="text-center fw-bolder">Tarefas</h1>
      </div>
    </div>
    <task-progress :progress="progress"></task-progress>
    <new-task @taskAdded="addTask"></new-task>
    <task-grid
      :tasks="tasks"
      @taskDeleted="deleteTask"
      @taskStateChanged="toggleTaskState"
    ></task-grid>
  </div>
</template>

<script>
import TaskGrid from "./components/TaskGrid.vue";
import NewTask from "./components/NewTask.vue";
import TaskProgress from "./components/TaskProgress.vue";
export default {
  components: { TaskGrid, NewTask, TaskProgress },
  data() {
    return {
      tasks: [],
    };
  },
  computed: {
    progress() {
      const total = this.tasks.length;
      const done = this.tasks.filter((t) => !t.pending).length;
      return Math.round((done / total) * 100) || 0;
    },
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
    },
  },
  methods: {
    addTask(task) {
      const sameName = (t) => t.name === task.name;
      const reallyNew = this.tasks.filter(sameName).length == 0;
      if (reallyNew) {
        this.tasks.push({
          name: task.name,
          pending: task.pending || true,
        });
      }
    },
    deleteTask(task) {
      this.tasks = this.tasks.filter((t) => t.name != task.name);
    },
    toggleTaskState(task) {
      var taskIndex = this.tasks.findIndex((t) => t.name === task.name);
      this.tasks[taskIndex].pending = !this.tasks[taskIndex].pending;
    },
  },
  created() {
    const json = localStorage.getItem("tasks");
    const array = JSON.parse(json);
    if (Array.isArray(array)) {
      this.tasks = array;
    } else {
      this.tasks = [];
    }
  },
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #fff;
}
</style>
