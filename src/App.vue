<template>
  <div class="container result__tiket">
      <ListBus
      v-bind:buses="buses"
      @viewTickets="Tikets"
    />
  </div>
</template>

<script>
import ListBus from './components/ListBus.vue';


export default {
  name: 'App',
  data(){
    return{
      buses:[]
    }
  },
  mounted(){
    fetch(' http://localhost:3000/bus')
    .then((response) => response.json())
    .then((json) => {
      this.buses = json;
    });

  },
  methods:{
    Tikets(object){
      console.log(object);
    }
  },
  components: {
    ListBus,
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
