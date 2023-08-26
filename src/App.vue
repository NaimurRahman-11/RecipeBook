<template>
 <div class="container">
  <HeadSection @toggle-add-recipe="toggleAddRecipe" :showAddRecipe="showAddRecipe" />
  <div v-if="showAddRecipe">
    <AddRecipe @add-recipe="addRecipe" />
  </div>
  <div class="mt-3">
      <button @click="toggleFilter" class="btn btn-primary">
        {{ showFavorites ? 'Show All' : 'Show Favorites' }}
      </button>
    </div>
  <Recipes :recipes="filteredRecipes" @delete-recipe="deleteRecipe"/>
  <Footer />
 </div>
</template>

<script>
import HeadSection from './components/HeadSection.vue'
import Footer from './components/Footer'
import Recipes from './components/Recipes'
import AddRecipe from './components/AddRecipe'
import Swal from 'sweetalert2';


export default {
  name: 'App',
  components: {
   HeadSection,
    Footer,
    Recipes,
    AddRecipe
  },
  
  data(){
    return{
      recipes:[],
      showAddRecipe: false,
      showFavorites: false,
    }
  },

methods:{

toggleFilter() {
      this.showFavorites = !this.showFavorites;
    },

  toggleAddRecipe(){
    this.showAddRecipe = !this.showAddRecipe
  },

  async addRecipe(recipe){
    const res = await fetch('http://localhost:5000/recipes', {
      method: 'POST',
      headers: {
        'Content-type': 'application/json',

      },
      body: JSON.stringify(recipe),
    })

    const data = await res.json()

    this.recipes = [...this.recipes, data]
  },


  async deleteRecipe(id){

 // Show a confirmation dialog using SweetAlert
      const result = await Swal.fire({
        title: 'Are you sure?',
        text: 'You will not be able to recover this recipe!',
        icon: 'warning',
        showCancelButton: true,
        confirmButtonText: 'Yes, delete it!',
        cancelButtonText: 'Cancel',
        reverseButtons: true,
      });

    if (result.isConfirmed) {
        const res = await fetch(`http://localhost:5000/recipes/${id}`, {
          method: 'DELETE',
        });

        if (res.ok) {
          // Remove the deleted recipe from the recipes array
          this.recipes = this.recipes.filter((recipe) => recipe.id !== id);
          // Show success alert
          Swal.fire({
            icon: 'success',
            title: 'Deleted!',
            text: 'Recipe has been deleted.',
          });
        } else {
          console.error('Failed to delete recipe');
        }
      }
  },

  async fetchRecipes(){
    const res = await fetch('http://localhost:5000/recipes')
    const data = await res.json()
    return data
  },

  async fetchRecipe(id){
    const res = await fetch(`http://localhost:5000/recipes/${id}`)
    const data = await res.json()
    return data
  }
},

 computed: {
    filteredRecipes() {
      if (this.showFavorites) {
        return this.recipes.filter(recipe => recipe.isFavorite);
      } else {
        return this.recipes;
      }
    },
  },

 async created(){
    this.recipes = await this.fetchRecipes()
  }
}
</script>

<style>

</style>
