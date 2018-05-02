<template>
    <!-- <img src="./assets/logo.png"> -->
  <div id="app">
    <div class="input">
      <div class="title">
        <h1>Cost</h1>
        <h1>Calculator</h1>
      </div>
      <CreateIngredient class='create' v-on:create-ingredient="createIngredient"/>
    </div>
    <div class="recipe">
      <h2>Recipe</h2>
      <List :recipe='recipe' v-on:send-to-buy="sendToBuy"> </List>
    </div>
    <div class="buylist">
      <h2>Buy List</h2>
      <Buylist :buylist='buylist'> </Buylist>
      <button @click='calcRatio(recipe, buylist)'>Servings</button>
      <div v-if="reaveal">
        <h4>You have enough ingredients to make at most {{this.min}} recipe.</h4>
        <div v-for="ingredient in this.ratios" :key="ingredient.name">
          <p>
            You have enough {{ingredient.name}} to make {{ingredient.ratio}} amount of recipe.
          </p>
        </div>
      </div>
    </div>
    <!-- <Converter /> -->
  </div>
</template>
<script>
import HelloWorld from './components/HelloWorld'
import CreateIngredient from './components/CreateIngredient'
import Ingredient from './components/Ingredient'
import Converter from './components/Converter'
import List from './components/List'
import Buylist from './components/Buylist'

export default {
  name: 'App',
  components: {
    HelloWorld,
    CreateIngredient,
    Ingredient,
    Converter,
    Buylist,
    List
  },
  data () {
    return {
      recipe: [],
      buylist: [],
      ratios: [],
      min: null,
      reaveal: false
    };
  },
  methods: {
    createIngredient (newIngredient) {
      if (newIngredient.buylist) {
        this.buylist.push(newIngredient);
      } else {
        this.recipe.push(newIngredient);
      }
      console.log('new: ' + newIngredient.buylist);
    },
    sendToBuy (dup) {
      console.log(dup[0].name + ' - ');
      this.buylist = [];
      for (let i = 0; i < dup.length; i++) {
        console.log(dup[i].name + ' - ' + dup[i].price);
        this.buylist.push(dup[i]);
      }
    },
    calcRatio (recipe, buylist) {
      this.reaveal = true
      this.ratios = []
      let temp_arr = []
      for (let i = 0; i < recipe.length; i++) {
        let temp = {}
        temp.name = buylist[i].name
        temp.ratio = buylist[i].size / recipe[i].size;
        this.ratios.push(temp)
        temp_arr.push(temp.ratio)
      }
      this.min = parseFloat(Math.round(Math.min(...temp_arr) * 100) / 100).toFixed(2)
    }
  }
}
</script>

<style scoped>

  .title {
    background-color: azure;
    grid-row: 1;
  }
  .create {
    background-color: slategray;
    grid-row: 2;
  }
  .input {
    background-color: #fff;
    display: grid;
    grid-template-rows: 1fr 1fr;
  }
  .recipe {
    background-color: #fff;
  }
  .buylist {
    background-color: #fff;
  }
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 80vh;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  /* grid-template-rows: repeat(3, 1fr); */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
