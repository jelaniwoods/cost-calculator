<template>
  <div id="app">
    <img src="./assets/logo.png">
    <List :recipe='recipe'> </List>
    <CreateIngredient v-on:create-ingredient="createIngredient"/>
    <Buylist :buylist='buylist'> </Buylist>
    <Converter />
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
