<template>
  <div>
    <label for="">Select a country from the dropdown list </label>
    <select name="" id="">
      <option value="" v-for="item in list" :key="item.id">
        {{ item.name }}
      </option>
    </select>

    <h2>World Statistics</h2>
    <div>
      <button>Sort by Country</button>
      <button>Sort by total cases(desc)</button>
      <button>Sort by Percentage of recovery(Asc)</button>
    </div>
    <table class="styleTable" border="1px">
      <tr>
        <td>Country</td>
        <td>Total Cases</td>
        <td>Percentage of recovery</td>
        <td>Percentage of death</td>
      </tr>
      <tr v-for="item in list" :key="item.id">
        <td>
          {{ item.name }}
        </td>
        <td>
          {{ item.total_cases }}
        </td>
        <td>{{ (item.recovery_ratio * 100).toFixed(2) }}</td>
        <td>{{ (item.death_ratio * 100).toFixed(2) }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios);
export default {
  name: "WorldStatistics",
  data() {
    return { list: undefined };
  },
  mounted() {
    Vue.axios
      .get("https://api.quarantine.country/api/v1/summary/latest")
      .then((resp) => {
        const array = [resp.data.data.regions];
        this.list = array[0];
      });
  },
};
</script>
