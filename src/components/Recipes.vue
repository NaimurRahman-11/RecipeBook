<template>
  <div class="row row-cols-1 row-cols-md-3 g-4 mt-5 mb-5">
    <div v-for="recipe in recipes" :key="recipe.id" class="col">
      <div class="card h-100">
        <img
          :src="recipe.image"
          class="card-img-top"
          alt="Recipe Image"
          :style="{ objectFit: 'cover', height: '250px' }"
        />
        <div class="card-body">
          <h5 class="card-title">{{ recipe.name }}</h5>
          <p class="card-text">{{recipe.description}}</p>
        </div>
        <div
          class="card-footer d-flex align-items-center justify-content-between"
        >
          <button class="btn btn-primary">View</button>
          <div>
            <i class="fa-solid fa-heart fa-lg me-5"></i>
            <i @click="onDelete(recipe.id)" class="fa-solid fa-trash fa-lg text-danger"></i>
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

  methods: {
    onDelete(id){
      this.$emit('delete-recipe', id)
    }
  },

};
</script>

<style>
</style>