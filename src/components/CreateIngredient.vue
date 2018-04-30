<template lang="html">
  <div class="create-ingredient">
    <div>
        <label>Name</label>
        <input v-model="name" type='text'>
        <br/>
        <label>Size (in oz)</label>
        <input v-model="size" type='text'>
        <br/>
        <label>Price</label>
        <input v-model="price" type='text'>
        <br/>
        <input v-model="buylist" type='checkbox'> Put this on BuyList
        <br/>
        <button v-on:click="sendForm" class="">
          Add To Recipe
        </button>
        
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
        name: "",
        size: 0,
        price: 0,
        buylist: false
    }
  },
  methods: {
    sendForm() {
      if (this.name.length > 0 && this.size > 0) {
        const name = this.name;
        const size = this.size;
        const price = this.price;
        const buylist = this.buylist;
        if (buylist) {
            this.$emit('create-ingredient', {
              name: this.name,
              size: this.size,
              price: this.price,
              buylist: true
            });
        }
        else {
            this.$emit('create-ingredient', {
              name: this.name,
              size: this.size,
              price: this.price
            });
        }
        this.name = '';
        this.size = 0;
        this.price = 0;
        this.buylist = false;
      } 
    } 
  }

}
</script>

<style lang="css" scoped>

</style>

