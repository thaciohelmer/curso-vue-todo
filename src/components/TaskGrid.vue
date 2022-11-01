<template>
  <div class="row px-4 justify-content-center">
    <template v-if="tasks.length">
      <task-item
        v-for="task in tasks"
        :key="task.name"
        :task="task"
        @taskDeleted="$emit('taskDeleted', task)"
        @taskStateChanged="$emit('taskStateChanged', task)"
      ></task-item>
    </template>
    <div class="col-12" v-else>
      <p class="mb-0 fs-4 text-center">Sua vida está em dia 😁</p>
    </div>
  </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";
export default {
  components: { TaskItem },
  props: {
    tasks: { type: Array, required: true },
  },
};
</script>

<style scoped>
</style>