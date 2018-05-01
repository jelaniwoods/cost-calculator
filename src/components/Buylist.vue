<template lang="html">
    <div class="list" v-if='buylist.length'>
        <ul>
            <li v-for="ingredient in buylist">
            <Ingredient :ingredient.sync="ingredient" />
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
</style>
