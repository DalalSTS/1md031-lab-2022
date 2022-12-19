<template>
    <div>
      <div class="box a">
        <p> {{this.burger.name}} <span>is orderd: </span> {{amountOrdered}}</p>
            <h3>{{burger.name}}</h3>
            <!-- v-bind:src= -->
            <img v-bind:src="burger.url" style="width:15em; height:20em">
            <ul>
              <li>{{burger.kCal}}</li>
              <span v-if="burger.lactose == true">
                <li>Contains <span class="certain">lactose</span></li>
              </span>
              <span v-if="burger.gluten == true">
                <li>Contains <span class="certain">gluten</span></li>
              </span>
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
      this.$emit('orderedBurgers', { 
                  name: this.burger.name,
                  amount: this.amountOrdered
          }
      );

    },
    removeBurger: function () {
      if (this.amountOrdered > 0){
      this.amountOrdered -= 1;
      this.$emit('orderedBurgers', { 
                  name: this.burger.name,
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
  