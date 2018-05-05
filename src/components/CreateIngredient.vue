<template lang="html">
  <div class="create-ingredient">
    <div class='input'>
      <div class='inps'>
        <label>Name</label>
        <input v-model="name" type='text'>
        <br/>
      </div>
      <div class='inps selector'>
        <label>Size (Select Units)</label>
        <input v-model="size" type='text'>
        <select v-model="unit">
            <option value="l">liter</option>
            <option value="ml">ml</option>
            <option value="kg">kg</option>
            <option value="g">g</option>
        </select>
        <br/>
      </div>
      <div class='inps'>
        <label>Price</label>
        <input v-model="price" type='text'>
        <br/>
      </div>
      <div class='inps'>
        <input v-model="buylist" type='checkbox'> Put this on BuyList
        <br/>
      </div>
        <button v-on:click="sendForm" class="addButt">
          Add To Recipe
        </button>
    </div>
    <p>Notes: for ingredients like eggs, or bread slices that have their own
      unique units you can choose any unit and just make sure the proportions are correct.
      (2ml of eggs in recipe and 12ml in buylist if the recipe requires 2 eggs and you buy a dozen at a time)
    </p>
  </div>
</template>
<script>
export default {
  data () {
    return {
      name: '',
      size: null,
      unit: null,
      price: null,
      buylist: false
    }
  },
  methods: {
    sendForm () {
      if (this.name.length > 0 && this.size > 0) {
        const name = this.name
        const size = this.size
        const unit = this.unit
        const price = this.price
        const buylist = this.buylist
        if (buylist) {
          this.$emit('create-ingredient', {
            name: this.name,
            size: this.size,
            unit: this.unit,
            price: this.price,
            edit: false,
            buylist: true
          })
        } else {
          this.$emit('create-ingredient', {
            name: this.name,
            unit: this.unit,
            size: this.size,
            edit: false,
            price: this.price
          })
        }
        this.name = null
        this.size = null
        this.unit = null
        this.price = null
        this.buylist = false
      }
    }
  }
}
</script>
<style lang="css" scoped>
  .input {
    border: 1px solid orange;
    padding: 1em;
    background-color: aliceblue;
  }
select {
    box-shadow: 2px 2px 0 #828181 inset;
    background-color: rgb(255, 255, 255);
    height: 28px;
    border-radius:5px;
    color: #1b1b1b;
    border: 0;

}
input[type=text]
{
    background-color: rgb(255, 255, 255);
    border:solid 1px rgb(255, 255, 255);
    color: #1b1b1b;
    border: 0;
    border-radius:5px;
    height: 28px;
    padding-left:10px;
    width: 191px;
    box-shadow: 2px 2px 0 #828181 inset;
}
  .inps {
    padding-bottom: .5em;
  }
</style>
