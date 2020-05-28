<template>

  <div class="hello">
    <h1>Vue.js Calorie Counter</h1>
    <div id="titles">
      <span>description </span>
      <span>calories</span>
      <span>fat</span>
      <span>carbs</span>
      <span>protein</span>
    </div>
        <ul>
          <li v-for="(item, index) in listOfItems" v-bind:key="index">
            <span>{{ item.name }}</span> |
            <span>{{ item.cal }}</span> |
            <span>{{ item.carbs }}</span> |
            <span>{{ item.fat }}</span> |
            <span>{{ item.protein }}</span>
            &nbsp;
            <button v-on:click="removeItem(index)">x</button>
          </li>

        </ul>

        <div id="totals">
          <span>Total: </span>
          <span>{{ totals.totalCal }}</span> |
          <span>{{ totals.totalCarbs }}</span> |
          <span>{{ totals.totalFat }}</span> |
          <span>{{ totals.totalProtein }}</span>
        </div>

        <div id="adding">
          <input v-bind:placeholder='placeholderValues.inputNameText' v-model="newValues.newName" type="text">
          <input v-bind:placeholder='placeholderValues.inputCalText' v-model="newValues.newCal" type="number">
          <input v-bind:placeholder='placeholderValues.inputCarbsText' v-model="newValues.newCarbs" type="number">
          <input v-bind:placeholder='placeholderValues.inputFatText' v-model="newValues.newFat" type="number">
          <input v-bind:placeholder='placeholderValues.inputProteinText' v-model="newValues.newProtein" type="number">
          <button v-on:click="addItem">+</button>
        </div>

  </div>


</template>


<script>
export default {
  name: 'HelloWorld',
  data: function () {
    return {


      placeholderValues: {
        inputNameText: 'Description',
        inputCalText: 'Calories',
        inputCarbsText: 'Carbs',
        inputFatText: 'Fat',
        inputProteinText: 'Protein',
      },


      newValues: {
        newName: '',
        newCal: '',
        newCarbs: '',
        newFat: '',
        newProtein: '',
      },

      
      listOfItems: [
        {
          name: 'Sargarepa',
          cal: 1000,
          carbs: 500,
          fat: 40,
          protein: 100
        },
        {
          name: 'Krompir',
          cal: 400,
          carbs: 503,
          fat: 17,
          protein: 200
        },
        {
          name: 'Paradajz',
          cal: 100,
          carbs: 100,
          fat: 10,
          protein: 320
        }
      ],
      totals: {
        totalCal: 0,
        totalCarbs: 0,
        totalFat: 0,
        totalProtein: 0
      }
    }
  },



  methods: {
    addItem: function () {

      this.listOfItems.push({
        name: this.newValues.newName,
        cal:  this.newValues.newCal,
        carbs:  this.newValues.newCarbs,
        fat:  this.newValues.newFat,
        protein:  this.newValues.newProtein
      });

        this.newName = '';
        this.newCal = '';
        this.newCarbs = '';
        this.newFat = '';
        this.newProtein = '';
        this.calcValues();
    },



    removeItem: function(itemIndex){
      this.listOfItems.splice(itemIndex, 1);
      this.calcValues();
    },
    calcValues: function () {
      for (let i = 0; i < this.listOfItems.length; i++) {
        this.totals.totalCal += parseInt (this.listOfItems[i].cal);
        this.totals.totalCarbs += parseInt (this.listOfItems[i].carbs);
        this.totals.totalFat += parseInt (this.listOfItems[i].fat);
        this.totals.totalProtein += parseInt (this.listOfItems[i].protein);
      }
    }
  }
}





</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
   .hello {
    max-width:950px;
    width:70%;
    margin: 0 auto;
    border:1px solid #000;
    position: relative;
    font-family: 'Arial', sans-serif;
    border-radius: 10px;
    h1{
      background-color:rgb(70, 161, 131);
      color: #fff;
      margin:0;
      padding:20px 0;
      text-align: center;
    }
    #titles {
      text-transform: uppercase;
      display:flex;
      justify-content: space-between;
      padding:14px 15px;
      border-bottom:1px solid gray;
      font-weight: bold;
      span {
        display:inline-block;
        width:100px;
        padding:5px 5px 5px 5px;
        &:nth-child(1){
          width:25%;
        }
      }
    }
    ul {
      padding:0;
      margin:0;
      padding:20px 34px;
      li{
        list-style-type: none;
        margin:0;
        padding:0;
        display:flex;
        justify-content: space-between;
        position:relative;
        padding-top:5px;
        span {
          display:inline-block;
          width:100px;
          padding:5px 0 2px 5px;
          border-bottom: 1px solid gray;
          &:nth-child(1){
            width:25%;
          }
        }
        button {
          position: absolute;
          right:-32px;
          bottom:0px;
          color:red;
          background-color: rgba(0,0,0,0);
          font-size: 20px;
          border:none;
          &:hover {
            cursor: pointer;
          }
        }
      }
    }
    #totals {
      display:flex;
      justify-content: space-between;
      padding:20px 24px;
      span {
        display: inline-block;
        padding-left: 5px;
        width:100px;
        font-weight: bold;
        font-size:20px;
        &:nth-child(1){
          width:25%;
          font-weight: normal;
        }
      }
    }
    #newItem {
      display: flex;
      justify-content: space-between;
      padding:20px 20px 30px;
      input {
        border:none;
        border-bottom:1px solid #333;
        width:100px;
        padding:5px 0 5px 10px;
        display:inline-block;
        &:nth-child(1){
            width:25%;
          }
      }
    }
  }
</style>










