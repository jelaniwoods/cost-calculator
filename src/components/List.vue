<template lang="html">
  <div>

      <div class="list" v-if='recipe.length'>
        <li v-for="ingredient in recipe">
          <Ingredient :ingredient.sync="ingredient" />
        </li>
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
  }
}
</script>
<style lang="css" scoped>
</style>
