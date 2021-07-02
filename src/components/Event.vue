<template>
    <div>
        <div class="card-container">
             <h3>{{title}}</h3>
             <p>{{description}}</p>
             <img class="imgCard" v-bind:src="image" alt="" >
             <button @click="showUsers(`${id}`); state = !state"  class="btn-card">{{state ? "hide users" : "show users"}}</button>
        </div>
        <div v-if="state" >
            <Subscribed v-for="user in subscribed" :key="user.index" :name="user.name"   />
            
        </div>
       
    </div>
</template>

<script>

import axios from 'axios'
import Subscribed from './Subscribed.vue'

export default {
   name: 'Event',
   props: ['title', 'description', 'id'],
  
   components: {
       Subscribed
   },

   data(){
       return{
           subscribed: [],
            state: false,
            image: " "
            
       }
       
   },

   mounted(){
       this.catchImageApi();
   },


   methods : {
       showUsers(id){
         axios.get(`http://127.0.0.1:8000/api/events/${id}/subscribed`).then(response => {
          this.subscribed = response.data
          !this.state
          
          })

       },

      catchImageApi(){
          axios.get(`http://127.0.0.1:8000/api/events/${this.id}/image`).then(response => {
            this.image = response.data
            console.log(this.image)
        })


      }
   }



}
</script>

<style scoped>
    .card-container{
        display:flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 40vh;
        max-width: 90vw;
        background-color: rgb(209, 228, 198) ;
        margin: 1rem auto;
        padding: 0.2rem 0;
        
    }

    .btn-card{
        font-size: 1rem;
        background-color: rgb(157, 189, 138);
        padding: 0.5rem 0.5rem;
        border:none;
        border-radius: 5px;
        cursor: pointer;
        transition: all ease 0.3s;
        
    }

    .btn-card:hover {
        background-color: rgb(157, 231, 113);
        
    }

    .imgCard{
        width: 8rem;
    }
</style>

