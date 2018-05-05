<template lang="html">
  <div class="ingredient">
      <h1 class="name" >
          <span v-if="!ingredient.edit">
            {{ingredient.name}}
          </span>
          <input v-if="ingredient.edit" v-model="ingredient.name">
      </h1>
      <p class="size">
          <span v-if="!ingredient.edit">
              {{ingredient.size}} {{ingredient.unit}}
          </span>
          <input v-if="ingredient.edit" v-model="ingredient.size" >
      </p>
      <p class="price" v-if='ingredient.buylist'>
          <span v-if="!ingredient.edit">
            ${{ingredient.price}}
          </span>
          <input v-if="ingredient.edit" v-model="ingredient.price" >
      </p>
  </div>
</template>
<script>
export default {
  props: ['ingredient']
}
</script>
<style lang="css" scoped>
    .ingredient h1, .ingredient p{
        display: inline-block;
        padding-right: 2em;
    }
    .ingredient {
        color: aliceblue;
        background: #1e1e1e;
    }
</style>
