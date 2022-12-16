<template>
  <div>
     <header>
      <div id="Header">
       <h1 id="Headline">Välkommen till BurgerOnline</h1>
       <img id="imgHeader" src="burger-sandwich-header.jpg">
      </div>
       
     </header>

     <main>

       <section id="section1">
         <h2>Select burger</h2>
         <p>This is where you execute burger selection</p>
         <div class="wrapper">

          <Burger v-for="burger in burgers" v-bind:burger="burger"
                v-bind:key="burger.name" />
          <!-- <div class="box a">
            <h3>The Fire Burger</h3>
            <img src="https://thumbs.dreamstime.com/b/burger-fire-black-background-site-171833764.jpg" style="width:15em; height:20em">
            <ul>
              <li>750 kCal</li>
              <li>Contains <span class="certain">lactose</span></li>
              <li>Contains <span class="certain">gluten</span></li>
            </ul>
          </div> -->
          <!-- <div class="box b">
            <h3>Fried Turkey Burger</h3>
            <img src="https://i0.wp.com/www.awortheyread.com/wp-content/uploads/2020/12/Deep-Fried-Turkey-Burger-17-681x1024.jpg" style="width:15em; height:20em">
            <ul>
              <li>600 kCal</li>
              <li>Contains <span class="certain">lactose</span></li>
              <li>Contains <span class="certain">gluten</span></li>
            </ul>
          </div>
          <div class="box c">
            <h3>A Double cheese burger</h3>
            <img src="https://www.foodiecrush.com/wp-content/uploads/2017/06/Bacon-Double-Cheddar-Cheeseburger-Caramelized-Onions-foodiecrush.com-015a-683x1024-1-500x500.jpg" style="width:15em; height:20em">
            <ul>
              <li>1800 kCal</li>
              <li>Contains <span class="certain">lactose</span></li>
              <li>Contains <span class="certain">gluten</span></li>
            </ul>
          </div>-->
         </div> 
         

       </section>
       <section id="section2">
         <h2>Customer information</h2>
         <p>This is where you provid necessary information</p>
         <form>
          <p>
           <label for="fullName">Full name</label> <br>
           <input type="text" v-model="name" required="required" id="fullName" placeholder="First- and Last name">
         </p>

         <p>
           <label for="email">E-mail</label> <br>
           <input type="email" v-model="em" required="required" id="email" placeholder="E-mail address">
         </p>

         <p>
           <label for="street">street</label> <br>
           <input type="text" v-model="sn" required="required" id="street" placeholder="Street name">
         </p>

         <p>
           <label for="house">House</label> <br>
           <input type="number" v-model="hn" required="required" id="house" placeholder="House number">
         </p>

         <p>
           <label for="payment">Payment methods</label>
           <select id="payment" v-model="pay">
             <option>Swish</option>
             <option>Cridet card</option>
             <option>Klarna</option>
             <option>Kontant</option>
           </select>
         </p>

         <p>
           Gender <br>
           <input type="radio" v-model="gender" value="male" id="male">
           <label for="male">Male</label> <br>
           <input type="radio" v-model="gender" value="female" id="female">
           <label for="female">Female</label> <br>
           <input type="radio" v-model="gender" value="donot" id="donot">
           <label for="donot">Do not wish to provide</label> <br>
         </p>
        </form>
       </section>
       <button type="submit" name="button" v-on:click="printForm">
         <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Bright_green_checkbox-checked.svg/1024px-Bright_green_checkbox-checked.svg.png" style="width:1em; height:1em">
         Send info
       </button>

       
         
     </main>

     <footer>
       <hr>
       <h5>&copy; Hypothetical Burgers Inc.</h5>
     </footer>
    </div>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'
import menu from '../assets/menu.json'

const socket = io();

function MenuItem(Bname, url, kCal, glut, lact) {
    this.name = Bname; 
    this.url = url;
    this.kCal = kCal;
    this.gluten = glut;
    this.lactose = lact;
    return this;
}

const Bur1 = new MenuItem("The Fire Burger", "https://thumbs.dreamstime.com/b/burger-fire-black-background-site-171833764.jpg", "750 kCal", "gluten", "lactose")
const Bur2 = new MenuItem("Fried Turkey Burger", "https://i0.wp.com/www.awortheyread.com/wp-content/uploads/2020/12/Deep-Fried-Turkey-Burger-17-681x1024.jpg", "600 kCal", "gluten", "lactose")
const Bur3 = new MenuItem("A Double cheese burger", "https://www.foodiecrush.com/wp-content/uploads/2017/06/Bacon-Double-Cheddar-Cheeseburger-Caramelized-Onions-foodiecrush.com-015a-683x1024-1-500x500.jpg", "1800 kCal", "gluten", "lactose")

let BArray = [ Bur1, Bur2, Bur3]


export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: menu
      
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
    },
    printForm: function () {
      console.log(
        this.name,
        this.em,
        this.sn,
        this.hn,
        this.pay,
        this.gender
      )
    }
  }
}
</script>

<style>

    @import 'https://fonts.googleapis.com/css?family=Pacifico|Dosis';

    body {
        font-family: arial;
    }

    .certain {
        font-weight: bold;
    }

    #section1 {
        background-color: black;
        color: white;
        border: 2px dashed white;	
    }

    #section2{
        border: 2px dashed black;
    }

    section{
        padding: 10px;
        margin: 2px;
    }

    button:hover {
        cursor: pointer;
        background-color: wheat;
    }
    

    button{
        margin: 2px;
    }

    div{
        padding: 2px;
        margin: 2px;
    }

    #imgHeader{
      width: 100%;
      height: 100%;
      opacity: 0.5;
    }

    #Headline{
      position: absolute;
      padding: 40px;
    }

    #Header{
      height: 200px;
      overflow:hidden;
      
    }

    .wrapper {
      display: grid;
      grid-gap: 10px;
      grid-template-columns: 33% 33% 33%;
    }


</style>