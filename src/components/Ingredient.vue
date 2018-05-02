<template lang="html">
  <div class="ingredient">
      <h1 class="name" >
          <span v-if="!ingredient.edit">
            {{ingredient.name}}
          </span>
          <input v-if="ingredient.edit" v-model="ingredient.name" >
      </h1>
          <!-- <input type="text" class="edit_item" v-model="item.title" 
          v-if="item.edit" ref='search' v-focus 
          v-on:keyup.enter="disableEdit(index)" 
          v-on:blur="disableEdit(index)"> -->
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
    props: ['ingredient'],
    data () {
        return {
        };
    },
    methods: {  
    }
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
