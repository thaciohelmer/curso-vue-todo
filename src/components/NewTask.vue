<template>
  <div class="row mb-4 justify-content-center">
    <div class="col-11 col-md-6">
      <div class="d-flex">
        <input
          type="text"
          class="form-control me-2"
          v-model="name"
          @keydown.enter="add"
        />
        <button class="btn btn-primary" @click="add">
          <i class="fa fa-plus" aria-hidden="true"></i>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
    };
  },
  methods: {
    add() {
      this.$emit("taskAdded", { name: this.name });
      this.name = "";
    },
  },
};
</script>

<style>
</style>