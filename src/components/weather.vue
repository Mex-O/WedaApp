<template>
  <div class="container-fluid" :id="weather.currentConditions?.temp?.c>37?'warm':''">
    <div class="row d-flex justify-content-center">
      <div class="col-lg-6">
        <input
          type="search"
          placeholder="Search..."
          v-model="query"
          @keypress="getWeather(e)"
        />
      </div>
      <div class="lg-12">
        <div class="weather">
          <div class="weather-title text-center">
            <img  v-show='this.show' @load="this.show=true" :src="weather.currentConditions?.iconURL" class="img-fluid" />
            <h3>{{ weather.currentConditions?.dayhour }}</h3>
            <h1>{{ weather.region }}</h1>
            <div
              class="temp"
              v-if="this.weather.currentConditions?.temp?.c > 1"
            >
              {{ weather.currentConditions?.temp?.c }}{{ this.degree }}
            </div>
            <h4>{{ weather.currentConditions?.comment }}</h4>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: "",
      weather: "",
      degree: "°c",
      show:false
    };
  },
  methods: {
    getWeather(e) {
        if(e='Enter'){
      fetch(`https://weatherdbi.herokuapp.com/data/weather/${this.query}`)
        .then((response) => response.json())
        .then((data) => (this.weather = data));
    }
    }
  },
};
</script>
<style>
body{
    width:100%;
    height:100%;
    overflow-x:hidden;
}
.container-fluid{
    background:url('../assets/bg.jpg');
    background-position:center;
    background-size:cover;
    min-height:150vh !important;
    padding:30px;
    background-repeat: no-repeat;
    margin:0;
    padding:0;
  } 
  #warm{
    background:url('../assets/hot.jpg');
    background-position:center;
    background-size:cover;
    min-height:150vh !important;
    padding:30px;
    background-repeat: no-repeat;
    margin:0;
    padding:0;
  }
input {
  width:100%;
  padding:18px;
  border-radius: 20px 20px !important;
  margin-top:none !important;
  border:none;
  font-size:larger;
  font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}
input:active {
  border: none !important;
}
.img-fluid {
  width: 200px;
  height: 200px;
}
.weather {
  margin: 100px;
  color:white;
}
.weather h1 {
  font-size: 30px;
}
.weather h3 {
  font-size: 20px;
  font-style: italic;
}
.weather h4 {
  font-size: 20px;
}
.weather .temp {
  margin: 10px;
  padding: 20px;
  font-size: 40px;
  font-weight: 900;
  text-align: center;
  justify-content: center;
  align-self: center;
}
</style>