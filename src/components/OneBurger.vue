<template>
    <div>
      <div class="box a">
        <p> Your nummber of orders is: {{amountOrdered}}</p>
            <h3>{{burger.name}}</h3>
            <!-- v-bind:src= -->
            <img v-bind:src="burger.url" style="width:15em; height:20em">
            <ul>
              <li>{{burger.kCal}}</li>
              <li>Contains <span class="certain">{{burger.lactose}}</span></li>
              <li>Contains <span class="certain">{{burger.gluten}}</span></li>
            </ul>

            <button type="button" v-on:click="addBurger">+Add</button>
            <button type="button" v-on:click="removeBurger">Remove-</button>
          </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'OneBurger',
    props: {
      burger: Object
    },
    data: function () {
      return {
        amountOrdered: 0,
      }
    },

    methods: {
    addBurger: function () {
      this.amountOrdered += 1;
      this.$emit('orderedBurger', { name:   this.burger.name,
            amount: this.amountOrdered
          }
      );
    },
    removeBurger: function () {
      if (this.amountOrdered > 0){
      this.amountOrdered -= 1;
      this.$emit('orderedBurger', { name:   this.burger.name,
            amount: this.amountOrdered
          }
      );
        }
    },
  }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  
  </style>
  