<template>
  <v-container class="grey lighten-5">
    <v-row class="mb-6">
      <v-col md="6">
        <v-card class="pa-2" outlined tile>City</v-card>
        <v-flex xs12 class="mt-4">
        <v-form @submit.prevent="getWeatherInfo">
            <v-text-field v-model="city" label="Enter City Name" solo></v-text-field>
        </v-form>
      </v-flex>
      </v-col>
      <v-col md="6">
        <v-card class="pa-2" outlined tile>Temperature</v-card>
        <v-flex xs12 class="mt-4">
        <v-card color="dark-grey darken-2">
          <v-card-text>
            <v-flex v-if="weather.weather" class="text-xs-center">
              <h4>Temperature</h4>
              <h2 class="display-1">{{weather.name}}</h2>
              <p>
                <span class="display-1">{{ Math.round(weather.main.temp) }} &deg;C</span>
                <span class="caption ml-4">{{ weather.weather[0].description }}</span>
              </p>
            </v-flex>
          </v-card-text>
        </v-card>
      </v-flex>
      </v-col>
    </v-row>
  </v-container>  
</template>
    

<script>
export default {

  name: 'WeatherPage',
  data(){
    return {
      city : "Ahmedabad",
      weather : {}
    }
  },
  
  created(){
    this.getWeatherInfo()
     
  },
  
  methods:{
    getWeatherInfo(){
      this.$axios.$get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=a1cf9ea5248a1e477bbbd3ef21652b1d`).then(res => (this.weather = res))
    }
  }
}

</script>