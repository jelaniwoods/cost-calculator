<template>
  <div id="app">
    <img src="./assets/logo.png">
    <HelloWorld/>
    <CreateIngredient v-on:create-ingredient="createIngredient"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import CreateIngredient from './components/CreateIngredient'
import Ingredient from './components/Ingredient'
import List from './components/List'

export default {
  name: 'App',
  components: {
    HelloWorld,
    CreateIngredient,
    Ingredient,
    List
  },
  data() {
    return {
      recipe: [{

      }],
      buylist: [{

      }]
    }
  },
  methods: {
    createIngredient(newIngredient) {
      if (newIngredient.buylist) {
        this.buylist.push(newIngredient);
      }
      else {
        this.recipe.push(newIngredient);
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
