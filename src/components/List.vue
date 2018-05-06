<template lang="html">
  <div>

      <div class="list">
        <ul v-if='recipe.length'>
          <li v-for="(ingredient, index) in recipe" @click="enableEdit(index)" @blur="disableEdit(index)">
            <div class="ingredient">
              <button class="butts" @click="deleteIngredient(index)">X</button>
              <br>
              <span v-if="!ingredient.edit" class='name'>
                {{ingredient.name}}
              </span>
              <input v-if="ingredient.edit" v-model="ingredient.name">
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
            </div>
          </li>
        </ul>
      </div>
    <button v-if="recipe.length" @click="sendToBuy">Duplicate in Buy</button>
  </div>
</template>
<script>
export default {
  props: ['recipe'],
  methods: {
    enableEdit (index) {
      this.recipe[index].edit = true
    },
    disableEdit (index) {
      this.recipe[index].edit = false
    },
    deleteIngredient (index) {
      this.recipe.splice(index, 1)
    },
    sendToBuy () {
      let dup = []
      for (let i = 0; i < this.recipe.length; i++) {
        dup[i] = {
          name: this.recipe[i].name,
          size: this.recipe[i].size,
          unit: this.recipe[i].unit,
          edit: this.recipe[i].edit,
          price: this.recipe[i].price,
          buylist: true
        }
        console.log(dup[0].name + ' xxx ' + this.recipe[0].name)
      }
      this.$emit('send-to-buy', dup)
    }
  }
}
</script>
<style lang="css" scoped>
  li {
   width: 300px;
   margin: 0 auto;
   list-style: none;
   text-align: center;
   margin-bottom: 1em;
  }
  .size {
    display: inline;
    padding-left: 2em;
  }
  .name {
    display: inline;
    padding-left: 2em;
  }
  .edit {
    display: inline;
    padding-left: 2em;  
  }
  .price {
    display: inline;
    padding-left: 2em;
  }
  .ingredient {
   background-color: rgba(122, 102, 102, 0.356);
   color: aliceblue;
   position: relative;
   padding: 1em;
  }
  .ingredient li {
    text-decoration: none;
  }
  .butts {
     position:absolute;
     top:0;
     right:0;
  }
</style>
