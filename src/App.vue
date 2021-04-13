<template>
  <div id="app">
    <h2>Covid-19 Dashboard by Sim Grewal</h2>
    <p>
      I confirm that the work submitted for grading is solely mine. While
      working on the take home exam, I neither recieved nor gave any assistance
      from/to other human beings. I understand that violating this academic
      honesty may seriously impact my grade for this class.
    </p>

    <div class="containerrr">
      <WorldStatistics />
      <TrendPerCountry v-bind:country="conutry" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import WorldStatistics from "./components/WorldStatistics";
import TrendPerCountry from "./components/TrendPerCountry";

export default {
  name: "App",
  components: {
    WorldStatistics,
    TrendPerCountry,
  },
  data() {
    return {
      list: undefined,
      conutry: null,
    };
  },

  mounted() {
    const getApiData = async () => {
      try {
        const options = {
          method: "GET",
          url: "https://coronavirus-map.p.rapidapi.com/v1/summary/latest",
          headers: {
            "x-rapidapi-key":
              "82cfa42bcamshdeb58c7ca825d3fp1cea0fjsnc2643a07e4bf",
            "x-rapidapi-host": "coronavirus-map.p.rapidapi.com",
          },
        };
        const res = await axios.request(options);
        this.list = res.data.data.regions;
        this.conutry = res.data.data.regions;
      } catch (error) {
        console.log(error);
      }
    };

    getApiData();
  },
  methods: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
.containerrr {
  display: flex;
}
</style>
