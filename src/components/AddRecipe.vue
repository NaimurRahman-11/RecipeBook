<template>
  <div class="container mt-5">
    <h2 class="mb-4">Add a New Recipe</h2>
    <form @submit.prevent="submitForm" class="row g-3">
      <div class="col-md-6">
        <label for="recipeName" class="form-label">Recipe Name</label>
        <input v-model="recipeName" type="text" class="form-control" id="recipeName" required>
      </div>
      <div class="col-md-6">
        <label for="photoUrl" class="form-label">Recipe Photo URL</label>
        <input v-model="photoUrl" type="text" class="form-control" id="photoUrl" required>
      </div>
      <div class="col-12">
        <label for="description" class="form-label">Description</label>
        <textarea v-model="description" class="form-control" id="description" rows="4" required></textarea>
      </div>
      <div class="col-12">
        <button type="submit" class="btn btn-primary">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddRecipe",
   data() {
    return {
      recipeName: '',
      photoUrl: '',
      description: ''
    };
  },

   methods: {
    submitForm() {
      const newRecipe = {
        name: this.recipeName,
        image: this.photoUrl,
        description: this.description
      };

      // Now you can do something with the new recipe data, like adding it to a list or sending it to a server.
      console.log(newRecipe);

      // Clear the form fields after submission
      this.recipeName = '';
      this.photoUrl = '';
      this.description = '';
    }
  }
};
</script>

<style>
</style>