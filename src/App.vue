<template>
  <div class="container result__tiket">
      <!-- <ListBus
      v-bind:buses="buses"
      @viewTickets="Tikets"
    /> -->
    <div v-if="component == 'ListBus'">
      <component :is="component" 
      v-bind:buses="buses"
      @viewTickets="Tikets"></component>
    </div>
    <div v-else>
      <component :is="component" 
      v-bind:tickets="tickets"
      @backBtn="BackBtn"
      ></component>
    </div>
    
  </div>
</template>

<script>
import ListBus from './components/ListBus.vue';
import Tiket from './components/Ticket.vue';

export default {
  name: 'App',
  data(){
    return{
      buses:[],
      tickets: [],
      component: 'ListBus'
    }
  },
  mounted(){
    fetch(' http://localhost:3000/bus')
    .then((response) => response.json())
    .then((json) => {
      this.buses = json;
    });
    fetch(' http://localhost:3000/tickets')
    .then((response) => response.json())
    .then((json) => {
      this.tickets = json;
    });

  },
  methods:{
    Tikets(object){
      console.log(object);
      this.component = 'Tiket'
    },
    BackBtn(){
      this.component = 'ListBus'
    }
  },
  components: {
    ListBus,
    Tiket
}
}
</script>

<style>
.container{
  max-width: 1344px !important;
  width: 1344px !important;
  margin: auto;
  position: relative;
}

.result__tiket{
  padding: 3rem 2rem !important;
  display: block;
}
</style>
