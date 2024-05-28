<template>
  <div class="wrapper">
    <h1>Weather App</h1>
    <p>Find out the weather in {{city == '' ? "your town" : cityName }}</p>
    <input type="text" v-model="city" placeholder="Enter town">

    <button v-if="city != ''" @click="getWeather()">Get weather</button>
    <button disabled v-else>Enter town name</button>

    <p class="error">{{ error }}</p>

    <div v-if="info != null">
      <p>{{ showTemp }} C</p>
      <p>{{ showFeelsLike }} C</p>
      <p>{{ showMinTemp }} C</p>
      <p>{{ showMaxTemp }} C</p>
    </div>

  </div>

  
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      city: '',
      error:'',
      info: null
    }
  },
  computed: {
    cityName() {
      return '"' + this.city + '"'
    },
    showTemp() {
      return "Temperature: " + this.info.main.temp;
    },
    showFeelsLike() {
      return "Feels like: " + this.info["main"]["feels_like"];
    },
    showMinTemp() {
      return "Minimal temp: " + this.info["main"]["temp_min"];
    },
    showMaxTemp() {
      return "Maximal temp: " + this.info["main"]["temp_max"];
    },
  },
  methods: {
    getWeather()
    {
        if(this.city.trim().length < 2) {
          this.error = "More than one symbol required."
          return;
        }

        this.error = '';

        axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=15a3b5b2354cfaa24d6470e77f466a49`)
          .catch(error => {
            if(error.code = 'ERR_BAD_REQUEST')
            {
              this.info = null;
              alert('City not found');
            }
          })
          .then(res => this.info = res.data);
    }
  }
}
 
</script>

<style scoped>
  .wrapper{
    width: 900px;
    height: 500px;
    border-radius: 50px;
    padding:20px;
    background: #1f0f24;
    text-align: center;
    color: white;
  }

  .wrapper h1{
    margin-top:50px;
  }

  .wrapper p{
    margin-top:20px;
   }

  .wrapper input {
    margin-top: 30px;
    background-color: transparent;
    border:0;
    border-bottom: 2px solid #110813;
    color: #fcfcfc;
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
  }

  .wrapper input:focus {
    border-bottom-color: #6e2d7d;
  }

  .wrapper button {
    background: #e3bc4b;
    color: #fff;
    border-radius: 10px;
    border: 2px solid #b99935;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: pointer;
    transition: transform 500ms ease;
  }

  .wrapper button:hover{
    transform: scale(1.1) translateY(-5px);
  }

  .wrapper button:disabled{
    background-color: #746027;
    cursor: not-allowed;
  }

  .error {
    color: rgb(147, 35, 35)
  }
</style>
