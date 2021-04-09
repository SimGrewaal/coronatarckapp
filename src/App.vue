<template>
  <div id="app">
    <h2>Covid-19 Dashboard by Sim Grewal</h2>
    <p>
      I confirm that the work submitted for grading is solely mine. While
      working on the take home exam, I neither recieved nor gave any assistance
      from/to other human beings. I understand that violating this academic
      honesty may seriously impact my grade for this class.
    </p>

    <WorldStatistics />
    <TrendPerCountry />
  </div>
</template>

<script>
import WorldStatistics from "./components/WorldStatistics";
import TrendPerCountry from "./components/TrendPerCountry";

export default {
  name: "App",
  components: {
    WorldStatistics,
    TrendPerCountry,
  },
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
</style>
