<template lang="html">
  <div>

      <div class="list" >
        <ul v-if='recipe.length'> 
          <li v-for="(ingredient, index) in recipe" @click="enableEdit(index)" @blur="disableEdit(index)">
            <div class="ingredient">
              <span v-if="!ingredient.edit">
                {{ingredient.name}}
              </span>
              <input v-if="ingredient.edit" v-model="ingredient.name" >
              <p class="size">
                  <span v-if="!ingredient.edit"> 
                      {{ingredient.size}} {{ingredient.unit}} 
                  </span>
                  <input v-if="ingredient.edit" v-model="ingredient.size" @keyup.enter="disableEdit(index)" @blur="disableEdit(index)"> 
                  <select v-if="ingredient.edit" v-model="ingredient.unit" @blur="disableEdit(index)">
                      <option value="l">liter</option>
                      <option value="ml">ml</option>
                      <option value="kg">kg</option>
                      <option value="g">g</option>
                  </select>
              </p>
              <p class="price" v-if='ingredient.buylist'>
                  <span v-if="!ingredient.edit"> 
                    ${{ingredient.price}}
                  </span>
                  <input v-if="ingredient.edit" v-model="ingredient.price" >
              </p>
              <button @click="deleteIngredient(index)">X</button>
            </div>
            <!-- <Ingredient :ingredient.sync="ingredient" /> -->
          </li>
        </ul>
      </div>

  </div>
</template>
<script>
import Ingredient from './Ingredient';
export default {
  props: ['recipe'],
  components: {
    Ingredient
  },
  data () {
    return {
    }
  },
  methods: {
    enableEdit(index) {
      this.recipe[index].edit = true;
    },
    disableEdit(index) {
      this.recipe[index].edit = false;
    },
    deleteIngredient(index) {
      this.recipe.splice(index, 1);
    }
  }
}
</script>
<style lang="css" scoped>
  li {
   width: 300px;
   margin: 0 auto;
  }
  .ingredient {
   background-color: #1e1e1e;
   color: aliceblue; 
  }
  .ingredient li {
    list-style-type: none;
    text-decoration: none;
  }
</style>
