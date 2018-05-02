<template>
  <div id="app">
    <img src="./assets/logo.png">
    <List :recipe='recipe' v-on:send-to-buy="sendToBuy"> </List>
    <CreateIngredient v-on:create-ingredient="createIngredient"/>
    <Buylist :buylist='buylist'> </Buylist>
    <Converter />
    <button @click='calcRatio(recipe, buylist)'>Servings</button>
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
  data() {
    return {
      recipe: [],
      buylist: []
    };
  },
  methods: {
    createIngredient(newIngredient) {
      if (newIngredient.buylist) {
        this.buylist.push(newIngredient);
      }
      else {
        this.recipe.push(newIngredient);
      }
      console.log('new: ' + newIngredient.buylist);
    },
    sendToBuy(dup) {
      console.log(dup[0].name + ' - ');
      this.buylist = [];
      for (let i = 0; i < dup.length; i++) {
        console.log(dup[i].name + ' - ' +dup[i].price);
        this.buylist.push(dup[i]);
      }
    },
    calcRatio(recipe, buylist) {
      /**
      take each matching ingredient from both lists
        divide buylist one from recipe one to get 
          how many servings of recipe can be made w/ that ingredient.
        then take the floor of all ratios to find most you can make w/ that buylist

        later can make more precise w/ fractions and returning each individual 
          ingredient ratios:
            x amount of eggs can make y amount of recipe                                                      
            b amount of flour can make c amount of recipe
       */
      console.log(recipe.length);
      let newlist = {};
      let temp = 0;
      for (let key in recipe) {
        if(recipe.hasOwnProperty(key)) {
          console.log(key + '- ' + recipe[key].name );
          temp = buylist[key].size / recipe[key].size;
          newlist[key] = {
            name: recipe[key].name,
            size: temp,
          }
        }
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
