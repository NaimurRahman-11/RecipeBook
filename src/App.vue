<template>
 <div class="container">
  <HeadSection />
  <AddRecipe />
  <Recipes :recipes="recipes" />
  <Footer />
 </div>
</template>

<script>
import HeadSection from './components/HeadSection.vue'
import Footer from './components/Footer'
import Recipes from './components/Recipes'
import AddRecipe from './components/AddRecipe'


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
      recipes:[]
    }
  },

  created(){
    this.recipes = [
      {
        id: 1,
        name: 'Beef Bhuna',
        image: 'https://cookbook.pfeiffer.net.au/files/beefBhuna.jpg'
      },
      {
        id: 2,
        name: 'Khashi Bhuna',
        image: 'https://uploads-ssl.webflow.com/5c481361c604e53624138c2f/5c5784dd46836abe97e82a07_kosha-mangsho-website-thumbnail-_p4nuue.png'
      },
      {
        id: 3,
        name: 'Murgi Bhuna',
        image: 'https://grubvineweb.com/wp-content/uploads/2022/08/Chicken-Bhuna-Masala-Recipe-Main-Image-Grubvineweb.webp'
      },
      {
        id: 4,
        name: 'Fish Curry',
        image: 'https://www.tamarindnthyme.com/wp-content/uploads/2020/10/Untitled-design-91-728x546.jpg.webp'
      }
    ]
  }
}
</script>

<style>

</style>
