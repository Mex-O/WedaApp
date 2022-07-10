<template>
  <div
    class="container-fluid"
    :id="weather.currentConditions?.temp?.c > 37 ? 'warm' : ''"
  >
    <div class="row d-flex justify-content-center">
      <div class="col-lg-12">
        <input
          type="search"
          placeholder="Search..."
          v-model="query"
          @keypress="getWeather(e)"
        />
      </div>
      <div class=" col-md text-center">
        <div class="weather">
          <div class="weather-title text-center">
            <img
              v-show="this.show"
              @load="this.show = true"
              :src="weather.currentConditions?.iconURL"
              class="img-fluid"
            />
            <h3>{{ weather.currentConditions?.dayhour }}</h3>
            <p>{{ weather.region }}</p>
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
      show: false,
    };
  },
  methods: {
    getWeather(e) {
      if ((e = "Enter")) {
        fetch(`https://weatherdbi.herokuapp.com/data/weather/${this.query}`)
          .then((response) => response.json())
          .then((data) => (this.weather = data));
      }
    },
  },
};
</script>
<style>
body {
  width:100%;
  overflow-x: hidden !important;
  font-family: "Times New Roman", Times, serif;
}
.container-fluid {
  background: url("../assets/bg.jpg");
  background-position: center;
  background-size: cover;
  height: 100rem !important;
  padding: 30px;
  background-repeat: no-repeat;
  margin: 0;
  padding: 0;
}
#warm {
  background: url("../assets/hot.jpg");
  background-position: center;
  background-size: cover;
  min-height: 100rem !important;
  padding: 30px;
  background-repeat: no-repeat;
  margin: 0;
  padding: 0;
}
input {
  width: 100%;
  padding: 18px;
  border-radius: 20px 20px !important;
  margin-top: 1px !important;
  border: none;
}
input:active {
  border: none !important;
}
.img-fluid {
  width: 200px;
  height: 200px;
}
.weather {
  margin: 150px;
  color: white;
}
.weather p {
  font-size: 25px;
  text-align:center;
  font-weight:bold;
}
.weather h3 {
  font-size: 20px;
  font-style: italic;
}
.weather h4 {
  font-size: 20px;
}
.weather .temp {
  padding: 5px;
  font-size: 40px;
  font-weight: 900;
  text-align: center;
  justify-content: center;
  align-self: center;
}
</style>