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
      <Buylist :buylist='buylist' v-on:get-sum='getSum'> </Buylist>
      <button @click='calcRatio(recipe, buylist)' v-if="buylist.length">Servings</button>
      <div v-if="reaveal">
        <h4>You have enough ingredients to make at most {{this.min}} recipe.</h4>
        <h4>The total cost of ingredients is: ${{this.sum}}</h4>
        <h5>The price per recipe is: ${{this.ppr}}</h5>
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
      reaveal: false,
      sum: 0,
      ppr: 0
    }
  },
  methods: {
    createIngredient (newIngredient) {
      if (newIngredient.buylist) {
        this.buylist.push(newIngredient)
      } else {
        this.recipe.push(newIngredient)
      }
      console.log('new: ' + newIngredient.buylist)
    },
    sendToBuy (dup) {
      console.log(dup[0].name + ' - ')
      this.buylist = []
      for (let i = 0; i < dup.length; i++) {
        console.log(dup[i].name + ' - ' + dup[i].price)
        this.buylist.push(dup[i])
      }
    },
    getSum (total) {
      console.log(total.total)
      this.sum = total.total
    },
    calcRatio (recipe, buylist) {
      // this.getSum();
      this.reaveal = true
      this.ratios = []
      let tempArr = []
      for (let i = 0; i < recipe.length; i++) {
        let temp = {}
        temp.name = buylist[i].name
        temp.ratio = buylist[i].size / recipe[i].size
        this.ratios.push(temp)
        tempArr.push(temp.ratio)
      }
      this.min = parseFloat(Math.round(Math.min(...tempArr) * 100) / 100).toFixed(2)
      this.ppr = parseFloat(this.sum / this.min).toFixed(2)
    }
  }
}
</script>

<style scoped>

  .title {
    background-color: rgb(136, 204, 204);
    grid-row: 1;
  }
  .create {
    background-color: slategray;
    padding-top: 4em;
    grid-row: 2;
  }
  .input {
    background-color: #fff;
    display: grid;
    grid-template-rows: 1fr 1fr;
  }
  .recipe {
    background-color: rgba(255, 68, 0, 0.527);
  }
  .buylist {
    background-color: rgba(53, 60, 155, 0.616);
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
