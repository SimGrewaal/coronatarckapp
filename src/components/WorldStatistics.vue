<template>
  <div>
    <h2>World Statistics</h2>
    <div>
      <button>Sort by Country</button>
      <button>Sort by total cases(desc)</button>
      <button>Sort by Percentage of recovery(Asc)</button>
    </div>
    <table class="styleTable">
      <thead>
        <tr>
          <th>Country</th>
          <th>
            Total <br />
            Cases
          </th>
          <th>
            Percentage of <br />
            recovery
          </th>
          <th>
            Percentage of <br />
            death
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in list" :key="item.id">
          <td>{{ item.name }}</td>
          <td class="total_cases">{{ item.total_cases }}</td>
          <td class="recovery">
            {{ (item.recovery_ratio * 100).toFixed(2) }}%
          </td>
          <td class="death">{{ (item.death_ratio * 100).toFixed(2) }}%</td>
        </tr>
      </tbody>
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
      } catch (error) {
        console.log(error);
      }
    };

    getApiData();
  },
};
</script>
<style >
.styleTable {
  border-collapse: collapse;
}
th,
td {
  border: 1px solid #ddd;
  padding: 10px;
}
.total_cases {
  text-align: right;
}
.recovery,
.death {
  text-align: center;
}
</style>


