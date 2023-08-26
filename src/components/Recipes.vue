<template>
  <div class="row row-cols-1 row-cols-md-3 g-5 mt-5 mb-5">
    <div v-for="recipe in recipes" :key="recipe.id" class="col ">
      <div class="card h-100 shadow">
        <img
          :src="recipe.image"
          class="card-img-top"
          alt="Recipe Image"
          :style="{ objectFit: 'cover', height: '250px' }"
        />
        <div class="card-body">
          <h5 class="card-title">{{ recipe.name }}</h5>
          <p class="card-text">{{ recipe.description }}</p>
        </div>
        <div
          class="card-footer d-flex align-items-center justify-content-between"
        >
          <button @click="openModal(recipe)" class="btn btn-primary">View</button>
          <div>
            <i class="fa-solid fa-heart fa-lg me-5"></i>
            <i
              @click="onDelete(recipe.id)"
              class="fa-solid fa-trash fa-lg text-danger"
            ></i>
          </div>
        </div>
      </div>
    </div>


 <!-- Modal for displaying recipe details -->
  <div class="modal fade" id="recipeModal" tabindex="-1" aria-labelledby="recipeModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="recipeModalLabel">{{ selectedRecipe.name }}</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <img :src="selectedRecipe.image" alt="Recipe Image" class="img-fluid mb-3" />
          <p>{{ selectedRecipe.description }}</p>
        </div>
      </div>
    </div>
  </div>


  </div>
</template>

<script>
export default {
  name: "Recipes",
  props: {
    recipes: Array,
  },

  data() {
    return {
      selectedRecipe: {}, // Store the selected recipe data
    };
  },

  methods: {
    onDelete(id) {
      this.$emit("delete-recipe", id);
    },

    openModal(recipe) {
      this.selectedRecipe = recipe; // Set the selected recipe data
      // Show the modal
      const modal = new bootstrap.Modal(document.getElementById('recipeModal'));
      modal.show();
    },
  },
};
</script>

<style scoped>
/* Add hover animation to the delete icon */
.fa-trash:hover {
  transform: scale(1.2); /* Increase the size on hover */
  transition: transform 0.3s ease-in-out; /* Apply smooth transition */
  cursor: pointer;
}

/* Add hover animation to other icons if needed */
.fa-heart:hover {
  transform: scale(1.2);
  color: red; /* Change color on hover */
  transition: color 0.3s ease-in-out; /* Apply smooth color transition */
  cursor: pointer;
}

.card {
  transition: transform 0.3s linear; /* Use linear transition for smoother in and out */
}

.card:hover {
  transform: scale(1.1);
}

</style>