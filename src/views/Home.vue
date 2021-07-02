<template>
  <div class="home">
    <!-- 
    <div v-for="user in subscribed" :key="user">
      {{user.name}}
      {{user.email}}
    </div> -->
    <Event v-for="event in events"  :key="event.index" :id="event.id" :title="event.title" :description="event.description"  />
    

    
  </div>
</template>



<script>

import axios from 'axios'
import Event from '../components/Event.vue'

export default {
  name: 'Home',
  components: {
    Event
  },

  data(){
    return {
       events: [],
       
    }
  },

  mounted() {
    
    this.catchApi();
    
  },

  methods : {
        catchApi(){
          axios.get('http://127.0.0.1:8000/api/events').then(response => {
        this.events = response.data
        })
      },

       
  }
     
}
</script>
