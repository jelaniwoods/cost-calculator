<template lang="html">
  <div class="ingredient">
      
  </div>
</template>
<script>
export default {
  data () {
    return {
        name: "",
        size: 0,
        price: 0
    }
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

</style>

