<template>
  <div>
    <div>
      Burgers
      <Burger v-for="burger in burgers"
              v-bind:burger="burger" 
              v-bind:key="burger.name"/>
    </div>
    <div id="map" v-on:click="addOrder">
      click here
    </div>
  </div>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'

const socket = io();

function MenuItem(Bname, url, kCal, glut, lact) {
    this.name = Bname; 
    this.url = url;
    this.kCal = kCal;
    this.gluten = glut;
    this.lactose = lact;
    return this;
}


let BArray = [new MenuItem("Burger1", "pic", "300", false, true)
, new MenuItem("Burger2", "pic", "400", false, true)
, new MenuItem("Burger3", "pic", "500", false, true)]

console.log (BArray)
export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: BArray
      
    }
    
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    }
  }
}
</script>

<style>
  #map {
    width: 300px;
    height: 300px;
    background-color: red;
  }
</style>