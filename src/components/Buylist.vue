<template lang="html">
    <div class="list" v-if='buylist.length'>
        <ul>
            <li v-for="(ingredient, index) in buylist" @click="enableEdit(index)" @blur="disableEdit(index)">
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
            </li>
        </ul>
        <div>
            <button @click='calc(buylist)'>calc </button>
            <div v-if='this.sum > 0'> ${{this.sum}}</div>
        </div>
    </div>
</template>
<script>
import Ingredient from './Ingredient';
export default {
  props: ['buylist'],
  components: {
    Ingredient
  },
  data () {
    return {
        sum: null
    }
  },
  methods: {
    enableEdit(index) {
      this.buylist[index].edit = true;
    },
    disableEdit(index) {
      this.buylist[index].edit = false;
    },
    deleteIngredient(index) {
      this.buylist.splice(index, 1);
    },
    calc(buylist) {
        let total = 0;
        for (let i = 0; i < buylist.length; i++) {
            total += parseInt(buylist[i].price);
        }
        this.sum = total;
        console.log(total + ' aaa00');
    }
  }
}
</script>
<style lang="css" scoped>
    li {
        width: 300px;
        margin: 0 auto;
        background-color: #999;
        display: inline-block;
    }
</style>
