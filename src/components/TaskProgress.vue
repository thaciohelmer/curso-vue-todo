<template>
  <div class="row mb-5">
    <div
      class="
        col-11
        justify-content-center
        mx-auto
        d-flex
        flex-column
        align-items-center
      "
    >
      <div class="tasks-progress">
        <span class="progress-value text-center">{{ progress }}%</span>
        <div
          class="progress-bar bg-success"
          :style="{ width: progress + '%' }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    progress: { type: Number, default: 0 },
  },
};
</script>

<style>
.tasks-progress {
  border: 1px solid #fff;
  border-radius: 2rem;
  width: 100%;
  height: 30px;
  position: relative;
  background-color: rgba(255, 255, 255, 0.3);
}

.progress-bar {
  border-radius: 2rem;
  height: 100%;
}

.progress-value {
  position: absolute;
  left: calc(50% - 25px);
  height: 100%;
  top: 2px;
  width: 50px;
}
</style>