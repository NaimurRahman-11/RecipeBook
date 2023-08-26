<template>
  <div
    class="header d-flex flex-column align-items-center justify-content-center"
  >
    <img
      src="https://mir-s3-cdn-cf.behance.net/project_modules/disp/0845c232253239.56766f2d063c9.gif"
      class="img-fluid"
      alt=""
    />
    <div class="d-flex p-2 align-items-center">
      <h1 class="text-center me-5">Recipe Book</h1>
      <button
        @click="$emit('toggle-add-recipe')"
        :class="{ 'btn-primary': !showAddRecipe, 'btn-danger': showAddRecipe }"
        class="btn"
      >
        {{ showAddRecipe ? "Close" : "Add Recipe" }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeadSection",
  props: {
    showAddRecipe: Boolean,
  },
  methods: {
    onClick() {
      this.$emit("btn-click");
    },
  },
};
</script>

<style>
</style>