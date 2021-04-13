<template>
  <div>
    <label for="">Select a country from the dropdown list </label>
    <select name="" id="list" v-on:change="myfun">
      <option value="">select country</option>
      <option v-for="item in country" :key="item.id">
        {{ item.name }}
      </option>
    </select>
    <h1>Trends in {{ demmmm || "India" }}</h1>

    <div>
      <button v-on:click="updateChart(demmmm || 'india', 'year')">
        Get Yearly Data
      </button>
      <button v-on:click="updateChart(demmmm || 'india', 'month')">
        Get Monthly Data
      </button>
      <button v-on:click="updateChart(demmmm || 'india', 'week')">
        Get Weekly Data
      </button>
    </div>
    <div class="box">
      <table class="styleTablew">
        <thead>
          <tr style="background: none">
            <th>Date</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in date" v-bind:key="item.id">
            <td>{{ item }}</td>
          </tr>
        </tbody>
      </table>
      <table class="styleTablew">
        <thead>
          <tr style="background: none">
            <th>Critical</th>
            <th>Deaths</th>
            <th>Deaths Ratio</th>
            <th>Recovery</th>
            <th>Recovery Ratio</th>
            <th>Total cases</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in list" :key="item.id">
            <td>{{ item.critical }}</td>
            <td>{{ item.deaths }}</td>
            <td>{{ item.death_ratio.toFixed(3) }}</td>
            <td>{{ item.recovered }}</td>
            <td>{{ item.recovery_ratio.toFixed(3) }}</td>
            <td>{{ item.total_cases }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <apexchart
      width="550"
      type="line"
      :options="chartOptions"
      :series="series"
    ></apexchart>
  </div>
</template>

<script>
import Vue from "vue";
import VueApexCharts from "vue-apexcharts";
import axios from "axios";

Vue.component("apexchart", VueApexCharts);
export default {
  name: "TrendPerCountry",
  props: ["country"],
  data() {
    return {
      demmmm: null,
      list: undefined,
      date: null,
      chartOptions: {
        chart: {
          id: "vuechart-example",
        },
        xaxis: {
          categories: [1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998],
        },
      },
      series: [
        {
          name: "series-1",
          data: [30, 40, 45, 50, 49, 60, 70, 81],
        },
      ],
    };
  },

  mounted() {
    const getApiData = async (cname) => {
      try {
        const options = {
          method: "GET",
          url: "https://coronavirus-map.p.rapidapi.com/v1/spots/week",
          params: { region: cname },
          headers: {
            "x-rapidapi-key":
              "82cfa42bcamshdeb58c7ca825d3fp1cea0fjsnc2643a07e4bf",
            "x-rapidapi-host": "coronavirus-map.p.rapidapi.com",
          },
        };
        const res = await axios.request(options);
        this.list = res.data.data;

        const objdata = res.data.data;
        console.log(objdata);
        var arr = [];
        var dates = [];
        for (const key in objdata) {
          const data = objdata[key].total_cases;
          arr.push(data);
          dates.push(key);
        }
        console.log(arr);
        console.log("asdasd", dates);
        this.date = dates;
      } catch (error) {
        console.log(error);
      }
      const newData = (this.series[0].data = arr.reverse());
      const year = (this.chartOptions.xaxis.categories = [...dates].reverse());
      this.chartOptions = {
        xaxis: {
          categories: year,
        },
      };
      this.series = [
        {
          data: newData,
        },
      ];
    };

    getApiData("india");
  },
  methods: {
    async myfun() {
      const selectedValue = document.getElementById("list").value;
      console.log(selectedValue);
      this.demmmm = selectedValue;
      try {
        const options = {
          method: "GET",
          url: "https://coronavirus-map.p.rapidapi.com/v1/spots/week",
          params: { region: selectedValue },
          headers: {
            "x-rapidapi-key":
              "82cfa42bcamshdeb58c7ca825d3fp1cea0fjsnc2643a07e4bf",
            "x-rapidapi-host": "coronavirus-map.p.rapidapi.com",
          },
        };
        const res = await axios.request(options);
        this.list = res.data.data;

        //=======
        const objdata = res.data.data;
        console.log(objdata);
        var arr = [];
        var dates = [];
        for (const key in objdata) {
          const data = objdata[key].total_cases;
          arr.push(data);
          dates.push(key);
        }
        console.log(arr);
        console.log(dates);
        this.date = dates;
      } catch (error) {
        console.log(error);
      }
      const newData = (this.series[0].data = arr.reverse());
      const year = (this.chartOptions.xaxis.categories = [...dates].reverse());
      this.chartOptions = {
        xaxis: {
          categories: year,
        },
      };
      this.series = [
        {
          data: newData,
        },
      ];
    },
    async updateChart(country_Name, country_Status) {
      try {
        const options = {
          method: "GET",
          url: `https://coronavirus-map.p.rapidapi.com/v1/spots/${country_Status}`,
          params: { region: country_Name },
          headers: {
            "x-rapidapi-key":
              "82cfa42bcamshdeb58c7ca825d3fp1cea0fjsnc2643a07e4bf",
            "x-rapidapi-host": "coronavirus-map.p.rapidapi.com",
          },
        };
        const res = await axios.request(options);
        this.list = res.data.data;

        //=======
        const objdata = res.data.data;
        console.log(objdata);
        var arr = [];
        var dates = [];
        for (const key in objdata) {
          const data = objdata[key].total_cases;
          arr.push(data);
          dates.push(key);
        }
        console.log(arr);
        console.log(dates);
        this.date = dates;
      } catch (error) {
        console.log(error);
      }
      const newData = (this.series[0].data = arr.reverse());
      const year = (this.chartOptions.xaxis.categories = [...dates].reverse());
      this.chartOptions = {
        xaxis: {
          categories: year,
        },
      };
      this.series = [
        {
          data: newData,
        },
      ];
    },
  },
};
</script>


<style >
.styleTablew {
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
.box {
  display: flex;
}
.styleTablew tr:nth-of-type(odd) {
  background: darksalmon;
}
.styleTablew tr:nth-of-type(even) {
  background: cyan;
}
</style>