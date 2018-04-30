<template lang="html">
  <div class="ingredient">
      <h1>{{ingredient.name}}</h1>
      <p>{{ingredient.size}}oz</p>
      <p v-if='ingredient.buylist'>${{ingredient.price}}</p>
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
      setName(newName) {
          this.name = newName; 
      },
      setSize(newSize) {
          this.size = newSize; 
      },
      setPrice(newPrice) {
          this.price = newPrice; 
      }
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

