<template>
    <div>
      <div class="box a">
            <h3>{{burger.name}}</h3>
            <!-- v-bind:src= -->
            <img v-bind:src="burger.url" style="width:15em; height:20em">
            <ul>
              <li>{{burger.kCal}}</li>
              <li>Contains <span class="certain">{{burger.lactose}}</span></li>
              <li>Contains <span class="certain">{{burger.gluten}}</span></li>
            </ul>
          </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'OneBurger',
    props: {
      burger: Object
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  
  </style>
  