<template>
    <v-app>
        <toolbar  :tool_name="title" :show="true"></toolbar>
         <v-btn color="blue" @click="$router.push('/')" outline>Back to main page</v-btn>
             <v-layout row wrap justify-center align-center mx-1 mt-2>
                 <div> <div v-for="i in image_src" :key="i" class="px-3" style="overflow:hidden;">
                   <v-img :src="i" height="200px" width="340px" ></v-img>
                  </div>
               <br>
                  
                   <p class="text-xs-center" style="font-size:20px">{{ image_name[0] }}</p>
                 </div>
                 
             </v-layout>
        <footnav></footnav>
    </v-app>
</template>

<script>
import toolbar from './toolbar.vue'
import fv from './fv'
import footnav from './footnav.vue'
import axios from 'axios'

export default {
  components:{
    toolbar,fv,footnav
           }, 
           data(){
                return{
                    title:'',
                    
                        image_name:['hackathon'],
                        image_src:[''],
                    
                    }
 },
 mounted(){
 var url = `http://192.168.43.158:8000`;
          axios.get(`${url}/cse/home`).then((res)=>{
              var temp_list = [];
              res.data.gallery.forEach(element => {
                  temp_list.push(`${url}${res.data.gallery}`);
              });
            this.image_src = temp_list;
            
          });
 }
 }
</script>
