<script setup>


</script>

<template>
<div class="container-vue">
  <h1 class="text">5 Day / 3 Hour Forecast Weather</h1> 
  <div class="grid-card">
    <div class="card" v-for="(i, index) in dataWeather.list" :key="index">
      <div class="container">
    <div class="cloud front">
      <span class="left-front"></span>
      <span class="right-front"></span>
    </div>
    <span class="sun sunshine"></span>
    <span class="sun"></span>
    <div class="cloud back">
      <span class="left-back"></span>
      <span class="right-back"></span>
    </div>
  </div>

  <div class="card-header">
    <span>{{ i.weather[0].main }}<br>{{i.weather[0].description}}</span>
    <span>{{ formatTimestamp(i.dt) }}</span>
  </div>
  <span class="temp">{{ i.main.temp.toFixed(1) }}</span>

  <div class="temp-scale">
    <span>Celcius</span>
  </div>
</div>
</div>
</div>
  </template>
  <script setup>
  
      import axios from 'axios'
      import { ref, onMounted } from 'vue'
  
      //import { ref } from 'vue'
  
      
      
      const dataWeather = ref({}) 
      const lat = ref("18.894855397965397")
      const long = ref("99.01081331585009")
      const api_key = ref("a6074756b0e9c16bf358232c10ba4e46")
  
      const url = ref('https://api.openweathermap.org/data/2.5/forecast?lat='+lat.value+'&lon='+long.value+'&appid='+api_key.value+'&units=metric')
  
  // fn format dateTime

      function formatTimestamp(timestamp) {
        const date = new Date(timestamp * 1000); 
          return date.toLocaleString(); 
        }


      function fetchPost() {
      axios
          .get(url.value)
          .then((respond)=>{
              dataWeather.value = respond.data;
              console.log(dataWeather.value)
          })
          .catch((err)=>{
              console.log(err)
          });
      }
      onMounted(fetchPost)
  
  </script>
  <style>
  .grid-card{
    display: grid;
    grid-template-columns: repeat(3,1fr);
    grid-gap: 3rem;
  }
  @media only screen and (max-width: 1100px) {
  .grid-card{
    grid-template-columns: repeat(2,1fr);
  }
}
@media only screen and (max-width: 750px) {
  .grid-card{
    grid-template-columns: repeat(1,1fr);
  }
}
  .container-vue{
    margin: 5rem auto;
    justify-content: center;
    justify-items: center;
  }
  .text{
    color: #3f3f3f;
    text-align: center;
    font-weight: 600;
    margin-bottom: 3.5rem;
  }
.card {
  width: 350px;
  height: 235px;
  position: relative;
  padding: 25px;
  background: radial-gradient(178.94% 106.41% at 26.42% 106.41%, #FFF7B1 0%, rgba(255, 255, 255, 0) 71.88%) /* warning: gradient uses a rotation that is not supported by CSS and may not behave as expected */, #FFFFFF;
  box-shadow: 0px 155px 62px rgba(0, 0, 0, 0.01), 0px 87px 52px rgba(0, 0, 0, 0.05), 0px 39px 39px rgba(0, 0, 0, 0.09), 0px 10px 21px rgba(0, 0, 0, 0.1), 0px 0px 0px rgba(0, 0, 0, 0.1);
  border-radius: 23px;
  transition: all 0.8s cubic-bezier(0.15, 0.83, 0.66, 1);
  cursor: pointer;
}

.card:hover {
  transform: scale(1.05);
}

.container {
  width: 250px;
  height: 250px;
  position: absolute;
  right: -35px;
  top: -50px;
  display: flex;
  align-items: center;
  justify-content: center;
  transform: scale(0.7);
}

.cloud {
  width: 170px;
}

.front {
  padding-top: 45px;
  margin-left: 30px;
  display: inline;
  position: absolute;
  z-index: 11;
  animation: clouds 8s infinite;
  animation-timing-function: ease-in-out;
}

.back {
  margin-top: -30px;
  margin-left: 163px;
  z-index: 12;
  animation: clouds 12s infinite;
  animation-timing-function: ease-in-out;
}

.right-front {
  width: 55px;
  height: 40px;
  border-radius: 50% 50% 50% 0%;
  background-color: #585858;
  display: inline-block;
  margin-left: -25px;
  z-index: 5;
}

.left-front {
  width: 65px;
  height: 65px;
  border-radius: 50% 50% 0% 50%;
  background-color: #585858;
  display: inline-block;
  z-index: 5;
}

.right-back {
  width: 50px;
  height: 50px;
  border-radius: 50% 50% 50% 0%;
  background-color:  #585858;
  display: inline-block;
  margin-left: -20px;
  z-index: 5;
}

.left-back {
  width: 35px;
  height: 30px;
  border-radius: 50% 50% 0% 50%;
  background-color: #585858;
  display: inline-block;
  z-index: 5;
}

.sun {
  width: 100px;
  height: 100px;
  margin-left: 50px;
  background: -webkit-linear-gradient(to right, #fcbb04, #fffc00);
  background: linear-gradient(to right, #fcbb04, #fffc00);
  border-radius: 60px;
  display: inline;
  position: absolute;
}

.sunshine {
  animation: sunshines 2s infinite;
}

@keyframes sunshines {
  0% {
    transform: scale(1);
    opacity: 0.6;
  }

  100% {
    transform: scale(1.4);
    opacity: 0;
  }
}

@keyframes clouds {
  0% {
    transform: translateX(15px);
  }

  50% {
    transform: translateX(0px);
  }

  100% {
    transform: translateX(15px);
  }
}

.card-header {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.card-header span:first-child {
  word-break: break-all;
  font-weight: 800;
  font-size: 15px;
  line-height: 135%;
  color: rgba(87, 77, 51, 0.66);
}

.card-header span:last-child {
  font-weight: 700;
  font-size: 15px;
  line-height: 135%;
  color: rgba(87, 77, 51, 0.33);
}

.temp {
  position: absolute;
  left: 25px;
  bottom: 12px;
  font-weight: 700;
  font-size: 64px;
  line-height: 77px;
  color: rgba(87, 77, 51, 1);
}

.temp-scale {
  width: 80px;
  height: 36px;
  position: absolute;
  right: 100px;
  bottom: 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.06);
  border-radius: 9px;
}

.temp-scale span {
  font-weight: 700;
  font-size: 15px;
  line-height: 134.49%;
  color: rgba(87, 77, 51, 0.66);
}

  </style>
