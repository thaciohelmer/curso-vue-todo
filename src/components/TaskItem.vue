<template>
  <div
    class="task rounded-3 d-flex justify-content-center py-4"
    :class="stateClass"
    @click="$emit('taskStateChanged', task)"
  >
    <span @click.stop="$emit('taskDeleted', task)"
      ><i class="fa fa-close" aria-hidden="true"></i
    ></span>
    <p class="text-center mb-0 fs-5">{{ task.name }}</p>
  </div>
</template>

<script>
export default {
  props: {
    task: { type: Object, required: true },
  },
  computed: {
    stateClass() {
      return {
        pending: this.task.pending,
        done: !this.task.pending,
      };
    },
  },
};
</script>

<style>
.task {
  box-sizing: border-box;
  cursor: pointer;
  user-select: none;
  width: 30%;
  margin: 1%;
  position: relative;
}

.task span {
  position: absolute;
  top: 5px;
  right: 5px;
  width: 20px;
  height: 20px;
  padding: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  background-color: rgba(0, 0, 0, 0.2);
  cursor: pointer;
}

.task span i {
  font-size: 10px;
}

.pending {
  background-color: #f44336;
  border-left: 12px solid #b73229;
}

.done {
  color: #ddd;
  border-left: 12px solid #0a8f08;
  background-color: #4caf50;
  text-decoration: line-through;
}

@media (min-width: 320px) {
  .task {
    width: 100%;
  }
}

@media (min-width: 480px) {
  .task {
    width: 45%;
  }
}

@media (min-width: 769px) {
  .task {
    width: 45%;
  }
}

@media (min-width: 1281px) {
  .task {
    width: 30%;
  }
}
</style>