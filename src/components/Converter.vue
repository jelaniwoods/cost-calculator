<template lang="html">
  <div class="coverter">
      <input v-model="item.amount">
      <select v-model="item.unit">
          <option value="ts"> ts</option>
          <option value="tbs"> tbs </option>
          <option value="oz"> oz</option>
          <option value="4cup"> 1/4 cup</option>
          <option value="3cup"> 1/3 cup</option>
          <option value="2cup"> 1/2 cup</option>
          <option value="cup"> 1 cup</option>
      </select>
      <button @click="convert(item)">Convert</button>
      <span v-if="item.newAmount != null">{{item.newAmount}} {{item.unit}}</span>
  </div>
</template>
<script>
export default {
    data () {
        return {
            item: {
                amount: null,
                unit: null,
                newAmount: null
            }
        }
    },
    methods: {
        convert(item) {
            switch (item.unit) {
                case "ts":
                    item.newAmount = item.amount * 5;
                    item.unit = 'ml'
                    console.log(item.newAmount + ' aaofjhfaoj');
                    break; 
                case "tbs":
                    item.newAmount = item.amount * 5;
                    item.unit = 'ml'
                    break; 
                case "oz":
                    item.newAmount = item.amount * 5;
                    item.unit = 'ml'
                    break; 
                case "4cup":
                    item.newAmount = item.amount * 5;
                    item.unit = 'ml'
                    break;
                case "3cup":
                    item.newAmount = item.amount * 5;
                    item.unit = 'ml'
                    break;
                case "2cup":
                    item.newAmount = item.amount * 5;
                    item.unit = 'ml'
                    break;
                case "cup":
                    item.newAmount = item.amount * 5;
                    item.unit = 'ml'
                    break;
                default: 
            }
        }
    }

}
</script>

<style lang="css" scoped>
</style>

