<template lang="html">
  <div class="create-ingredient">
    <div>
        <label>Name</label>
        <input v-model="name" type='text'>
        <br/>
        <label>Size (Select Units)</label>
        <input v-model="size" type='text'>
        <select v-model="unit">
            <option value="l">liter</option>
            <option value="ml">ml</option>
            <option value="kg">kg</option>
            <option value="g">g</option>
        </select>
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
        size: null,
        unit: null,
        price: null,
        buylist: false
    }
  },
  methods: {
    sendForm() {
      if (this.name.length > 0 && this.size > 0) {
        const name = this.name;
        const size = this.size;
        const unit = this.unit;
        const price = this.price;
        const buylist = this.buylist;
        if (buylist) {
            this.$emit('create-ingredient', {
              name: this.name,
              size: this.size,
              unit: this.unit,
              price: this.price,
              edit: false,
              buylist: true
            });
        }
        else {
            this.$emit('create-ingredient', {
              name: this.name,
              unit: this.unit,
              size: this.size,
              edit: false,
              price: this.price
            });
        }
        this.name = null;
        this.size = null;
        this.unit = null;
        this.price = null;
        this.buylist = false;
      } 
    } 
  }

}
</script>

<style lang="css" scoped>

</style>

