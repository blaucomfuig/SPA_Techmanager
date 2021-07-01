<template>
    <div>
        <div class="card-container">
             <h3>{{title}}</h3>
             <p>{{description}}</p>
             <button @click="showUsers(`${id}`)"  class="btn-card">subscribed users</button>
        </div>
        <div v-if="showUsers" >
            <p v-for="user in subscribed" :key="user">
                {{user.name}}
            </p>
        </div>
       
    </div>
</template>

<script>

import axios from 'axios'

export default {
   name: 'Event',
   props: ['title', 'description', 'id'],

   data(){
       return{
           subscribed: []
       }
       
   },

   methods : {
       showUsers(id){
         axios.get(`http://127.0.0.1:8000/api/events/${id}/subscribed`).then(response => {
          this.subscribed = response.data
          
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
        height: 25vh;
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
</style>

