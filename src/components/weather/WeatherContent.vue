<template>
  <div class="weather-wrapper">
    <ContentHeader />
    <CitySelector @selectCity="selectCity" />
    <WeatherList :weatherList="weatherList" />
  </div>
</template>

<script>
import weatherMixin from "@/mixins/weatherMixin";
import ContentHeader from "./ContentHeader.vue";
import CitySelector from "./CitySelector.vue";
import WeatherList from "./WeatherList.vue";
export default {
  name: "WeatherContent",
  mixins: [weatherMixin],
  components: { ContentHeader, CitySelector, WeatherList },
  data() {
    return {
      weatherList: [],
    };
  },
  methods: {
    async selectCity(city) {
      if (city.selected) {
        const weather = await this.getWeatherInfo(city);

        this.weatherList.push(weather);
      } else {
        const index = this.weatherList.findIndex(
          (weather) => weather.code === city.code
        );
        this.weatherList.splice(index, 1);
      }
      console.log(city, "parent received");
    },
  },
};
</script>

<style></style>
