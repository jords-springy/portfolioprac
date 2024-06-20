<template>
  <div>
    <h1>Counter -> <span>{{ counter }}</span></h1>
    <button @click="increment()"><span>Increment</span></button>
    <button @click="decrement()"><span>Decrement</span></button>
  </div>
  <img :src="imgUrl">
  <div>
    <!-- Class style binding -->
    <h4 :class="{hello:check}">Conditional rendering</h4>
    <!-- Conditional rendering -->
    <h1 v-if="check">The value is true</h1>
    <h1 v-else>The value is false</h1>
    <button @click="change()"><span>Change state</span></button>
    <h1 v-show="check">This got that v v-show</h1>
    <ul>
      <!-- list rendering -->
      <li v-for="(sport, index) in sports" :key="index">{{ sport }}</li>
      <li v-for="object in objects" :key="object.id">{{ object.message }}</li>
    </ul>
    <!-- one way data binding-->
    <h3>{{oneWayText}}</h3>
    <!-- two way data binding-->
    <h3>{{ twoWayText }}</h3>
    <input type="text" v-model="twoWayText">
  </div>
  <!-- <info-comp first-name="hehe" last-name="hehehehhehe"/>
  <info-comp first-name="hehe1"/>
  <info-comp :object-data="singleObject"/> -->
  <info-comp>
    Hehe I am using slots
  </info-comp>
  <slot-comp>
    <template #slotTitle>
      <!-- Card Slot -->
    </template>
    <template #default>
      <!-- <img :src="imgUrl"> -->
    </template>
  </slot-comp>
</template>

<script>
import InfoComp from '@/components/InfoComp.vue';
import SlotComp from '@/components/SlotComp.vue';
export default {
  data() {
    return {
      counter: 0,
      imgUrl: 'https://www.hollywoodreporter.com/wp-content/uploads/2019/11/the_end_of_the_fing_world_still.jpg?w=1296',
      check: true,
      sports: ['soccer', 'rugby', 'darts'],
      objects: [
        { message: "hello there 1", id: 1 },
        { message: "hello there 2", id: 2 },
        { message: "hello there 3", id: 3 }
      ],
      singleObject: {
        name: 'Jordan',
        surname: 'Springveldt'
      },
      oneWayText: 'hehe',
      twoWayText: 'hehe2.0',
    
    }
  },
  components: {
    InfoComp,
    SlotComp
  },

  methods: {
    increment() {
      this.counter++
    },
    decrement() {
      this.counter--
    },
    change() {
      this.check = !this.check
    }
  }
}
</script>

<style scoped>
img {
  width:300px;
  height:300px
}
  button {
    position: relative;
    overflow: hidden;
    background-color: rgb(29, 29, 29) !important;
    color: #fff !important;
    border-color: rgb(29, 29, 29) !important;
    font-family: "Noto Serif Display", serif;
    font-optical-sizing: auto;
    font-weight: 600;
    font-style: normal;
    font-variation-settings: "wdth" 100;
    text-align: center !important;
    padding: 10px 30px;
    cursor: pointer;
    transition: color 0.5s ease;
    border-radius: 0 !important;
    z-index: 1;
    will-change: color;
    margin: 10px
  }
  button::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: #42B983;
    z-index: 0;
    transition: transform 0.5s ease;
    transform: scaleX(0);
    transform-origin: left;
    backface-visibility: hidden; /* Prevent rendering issues */
    will-change: transform; /* Hint to the browser to optimize */
  }
  button:hover::before {
    transform: scaleX(1);
  }
  button:hover {
    color: #fff !important; /* Ensure text stays visible */
  }
  button span {
    position: relative;
    z-index: 2;
    backface-visibility: hidden; /* Prevent rendering issues */
    will-change: color; /* Hint to the browser to optimize */
  }

</style>