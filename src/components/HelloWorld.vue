
<template>
    <div>
        <ul v-for="event in events" v-bind:key="event">
            <li>{{event.title}}</li>
        </ul>
       
    </div>
    
</template>




<script>


export default {
  name: 'HelloWorld',
    data(){
        return {
            events: []
        }
    }, 
    mounted() {
        axios.get('http://127.0.0.1:8000/api/events').then(response => {
            this.events = response.data;
        });
    
   
    }


}
</script>