<template lang="html">
    <div class="list" v-if='buylist.length'>
        <ul>
            <li v-for="(ingredient, index) in buylist" :key="ingredient.name" @click="enableEdit(index)">
                <div class="ingredient">
                  <button class='butts' @click="deleteIngredient(index)">X</button>
                  <span v-if="!ingredient.edit" class='name'>
                      {{ingredient.name}}
                  </span>
                  <input v-if="ingredient.edit" v-model="ingredient.name" @blur="disableEdit(index)">
                  <p class="size">
                      <span v-if="!ingredient.edit">
                          {{ingredient.size}} {{ingredient.unit}}
                      </span>
                      <input v-if="ingredient.edit" v-model="ingredient.size"  @blur="disableEdit(index)" class='size'>
                      <select v-if="ingredient.edit" v-model="ingredient.unit" @blur="disableEdit(index)" class='edit'>
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
                      <input v-if="ingredient.edit" v-model="ingredient.price" @blur="disableEdit(index)">
                  </p>
                </div>
            </li>
        </ul>
        <div>
            <br/>
            <br/>
            <button @click='calc(buylist)'>Calculate Total Price</button>
            <br/>
            <br/>
            <div v-if='this.sum > 0'> ${{this.sum}}</div>
            <div v-if='!this.ready'>Pls make sure all ingredients have a price</div>
            <br/>
            <br/>
        </div>
    </div>
</template>
<script>
export default {
  props: ['buylist'],
  data () {
    return {
      sum: null,
      ready: true
    }
  },
  methods: {
    enableEdit (index) {
      this.buylist[index].edit = true
    },
    disableEdit (index) {
      this.buylist[index].edit = false
    },
    deleteIngredient (index) {
      this.buylist.splice(index, 1)
    },
    isReady (buylist) {
      for (let i = 0; i < buylist.length; i++) {
        // console.log(isNaN(buylist[i].price)  + '-' + buylist[i].price.length);
        if (buylist[i].price === null || isNaN(buylist[i].price) || buylist[i].price.length === 0) {
          return false
        }
      }
      console.log('um so we good?')
      return true
    },
    calc (buylist) {
      console.log('hewwo ' + this.ready)
      if (!this.isReady(buylist)) {
        this.ready = false
        console.log(this.ready + 'should be error')
      } else {
        this.ready = true
        let total = 0
        for (let i = 0; i < buylist.length; i++) {
          total += parseInt(buylist[i].price)
        }
        this.sum = total
        this.$emit('get-sum', {
          total: total
        })
      }
    }
  }
}
</script>
<style lang="css" scoped>
    li {
        width: 300px;
        margin: 0 auto;
        background-color: rgba(185, 179, 179, 0.034);
        list-style: none;
        margin-bottom: 1em;
    }
    .size {
      display: inline;
      padding-left: 2em;
    }
    .name {
      display: inline;
      padding-left: 2em;
    }
    .edit {
      display: inline;
      padding-left: 2em;  
    }
    .price {
      display: inline;
      padding-left: 2em;
    }
  .ingredient {
   background-color: rgba(207, 207, 207, 0.295);
   color: aliceblue;
   position: relative;
   padding: 1em;
  }
  .butts {
     position:absolute;
     top:0;
     right:0;
  }
</style>
