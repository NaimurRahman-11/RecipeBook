<template>
  <div class="container mt-2 mb-5 shadow p-3">
    <h2 class="mb-4">Add a New Recipe</h2>
    <form @submit="onSubmit" class="row g-3">
      <div class="col-md-6">
        <label for="recipeName" class="form-label fw-bold">Recipe Name</label>
        <input
          v-model="recipeName"
          type="text"
          class="form-control"
          id="recipeName"
          required
        />
      </div>
      <div class="col-md-6">
        <label for="photoUrl" class="form-label fw-bold"
          >Recipe Photo URL</label
        >
        <input
          v-model="photoUrl"
          type="text"
          class="form-control"
          id="photoUrl"
          placeholder="Paste the image address of your recipe"
          required
        />
      </div>
      <div class="col-12">
        <label for="description" class="form-label fw-bold">Description</label>
        <textarea
          v-model="description"
          class="form-control"
          id="description"
          rows="4"
          placeholder="Write a short description of your recipe (Maximum 70 Words)"
          maxlength="350"
          required
        ></textarea>
      </div>

      <div class="col-12">
        <label for="ingredients" class="form-label fw-bold">Ingredients</label>
        <textarea
          v-model="ingredients"
          class="form-control"
          id="ingredients"
          rows="4"
          placeholder="List your ingredients: (Example)
• 2 tablespoons Olive Oil
• 2 Cloves Garlic
• 1 can (400g) Crushed Tomatoes
• 1 teaspoon Dried Basil
• 1 teaspoon Dried Oregano
• Salt and Pepper to taste
• Grated Parmesan Cheese for garnish"
          required
        ></textarea>
      </div>

      <div class="col-12">
        <button type="submit" class="btn btn-primary">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
import Swal from "sweetalert2";

export default {
  name: "AddRecipe",
  data() {
    return {
      recipeName: "",
      photoUrl: "",
      description: "",
      ingredients: "",
    };
  },

  methods: {
    onSubmit(e) {
      e.preventDefault();

      const newRecipe = {
        name: this.recipeName,
        image: this.photoUrl,
        description: this.description,
        ingredients: this.ingredients.split("\n"),
      };

      // Now you can do something with the new recipe data, like adding it to a list or sending it to a server.
      console.log(newRecipe);

      this.$emit("add-recipe", newRecipe);

      Swal.fire({
        icon: "success",
        title: "Success",
        text: "Recipe added successfully!",
        ingredients: this.ingredients.split("\n"),
      });

      // Clear the form fields after submission
      this.recipeName = "";
      this.photoUrl = "";
      this.description = "";
      this.ingredients = "";
    },
  },
};
</script>

<style>
</style>