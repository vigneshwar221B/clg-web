<template>
    <v-app>
        <toolbar  :tool_name="title" :show="true"></toolbar>
        
            <v-btn color="blue" outline round @click="$router.push('/events')"><v-icon class="pr-1">replay</v-icon> Back To Event Page </v-btn>
        <v-container>
            <v-img :src="img_src"  aspect-ratio="1.8"></v-img>
            <h2>{{ event_name }}</h2>
            <p>{{ event_details }}</p>
        </v-container>

    </v-app>
</template>

<script>
import toolbar from './toolbar.vue'
import footnav from './footnav.vue'
import 'bootstrap'
import "bootstrap/dist/css/bootstrap.min.css"
import fv from './fv'
import pdf from 'vue-pdf'

import axios from 'axios'


export default {
    components:{
        toolbar,fv,footnav,pdf
    },
    props:['pk'],
    data(){
        return{
            title: '- CSE DEPARTMENT',
            event_name: "avantaa",
            img_src:'',
            event_details: "I take immense pleasure in inviting you all on behalf of 'sri krishna college of technology' to the avantta held on 11.03.2017 .."
        }},
        mounted(){
             var url = `http://192.168.43.158:8000`;
            axios.get(`${url}/event/${this.$route.params.pk}/`).then((res)=>{
              console.log(res);
              this.event_name = res.data.name;
              this.event_details = res.data.description;
              this.img_src = `${url}${res.data.image}`
                  });
              }
     
}




</script>


<style scoped>






</style>
