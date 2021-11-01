<template>
    <div class="input-group mb-3">
        <input type="text" v-model.lazy="city" class="form-control" placeholder="enter city">
        <button class="btn btn-success" @click="getpost" type="submit">Go</button>
    </div>
   
    <div class="card" style="width:2    00px">
    <div class="card-body" v-show="value">
        <img class="card-img-top"  src="../assets/bech.jpg" alt="Card image">
        <h4 class="card-title">Max Temp</h4>
        <p class="card-text">{{data.temp_max}}</p>
         <h4 class="card-title">Min Temp</h4>
        <p class="card-text">{{data.temp_min}}</p>
    </div>
    </div>
</template>

<script>
import { reactive, toRefs } from 'vue'
import axios from 'axios'
export default{
    name:'Input',
    setup(){
        const state=reactive({
            value:false,
            city:'',
            URL : 'https://api.openweathermap.org/data/2.5/weather',
            API_KEY : 'f33a484cf794d08d0148764789aaba32',
            data:{                            
                "temp": 0,
                "feels_like": 0,
                "temp_min": 0,
                "temp_max": 0,
                "pressure": 0,
                "humidity": 0
            }
                        
        })
        function getpost(){
             axios.get(state.URL, {
                    params: {
                        q: state.city,
                        units: 'metric',
                        APPID: state.API_KEY,
                    }
                }).then(res=>{
                    state.data=res.data.main
                    state.value = true
                }).catch(e=>{
                    console.log(e)
                })
              
            }
        
        return{
            getpost,
            ...toRefs(state)
        }
    }
}


</script>
