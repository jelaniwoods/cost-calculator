<template lang="html">
  <div class="coverter">
      <label>Amount</label>

      <input v-model="item.amount">
      <label>Unit</label>
      <select v-model="item.unit">
          <option value="ts"> ts</option>
          <option value="tbs"> tbs </option>
          <option value="floz"> fluid oz</option>
          <option value="oz"> oz</option>
          <option value="4cup"> 1/4 cup</option>
          <option value="3cup"> 1/3 cup</option>
          <option value="2cup"> 1/2 cup</option>
          <option value="cup"> cup</option>
      </select>
      <label>New Unit</label>
      <select v-model="item.newUnit" >
          <option value="l">liter</option>
          <option value="ml">ml</option>
          <option value="kg">kg</option>
          <option value="g">g</option>
      </select>
      <button @click="convert(item)">Convert</button>
      <span v-if="item.newAmount != null">{{item.newAmount}} {{item.newUnit}}</span>
  </div>
</template>
<script>
export default {
    data () {
        return {
            item: {
                amount: null,
                unit: null,
                newAmount: null,
                newUnit: null
            }
        }
    },
    methods: {
        convert(item) {
            switch (item.unit) {
                case "ts":
                    item.newAmount = item.amount * 5;
                    item.unit = 'ml';
                    break; 
                case "tbs":
                    item.newAmount = item.amount * 15;
                    item.unit = 'ml';
                    break; 
                case "floz":
                    item.newAmount = item.amount * 30;
                    item.unit = 'ml';
                    break; 
                case "oz":
                    item.newAmount = item.amount * 28;
                    item.unit = 'g';
                    break; 
                case "4cup":
                    item.newAmount = item.amount * 60;
                    item.unit = 'ml';
                    break;
                case "3cup":
                    item.newAmount = item.amount * 80;
                    item.unit = 'ml';
                    break;
                case "2cup":
                    item.newAmount = item.amount * 120;
                    item.unit = 'ml';
                    break;
                case "cup":
                    item.newAmount = item.amount * 240;
                    item.unit = 'ml'
                    break;
                default: 
            }
        },
        toMl(item) {
            switch (item.unit) {
                case "ts":
                    item.newAmount = item.amount * 5;
                break; 
                case "tbs":
                break; 
                case "floz":
                break; 
                case "4cup":
                break; 

            }
            item.newAmount = item.amount * 5;
            item.newUnit = 'ml';
        },
        toL(item) {
            item.newAmount = item.amount * 5;
            item.newUnit = 'l';

        },
        toOz(item) {
            item.newAmount = item.amount * 5;
            item.newUnit = 'l';

        }
    }

}
</script>

<style lang="css" scoped>
</style>

