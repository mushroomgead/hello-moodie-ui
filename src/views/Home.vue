<template>
  <apexchart
    width="500"
    height="300"
    type="heatmap"
    :options="chartOptions"
    :series="series"
  ></apexchart>
  <ul>
    <li v-for="item in items" :key="item.id">
      {{ item.created_date }} | {{ item.status }}
    </li>
  </ul>
  <button v-on:click="handleOnAdd">add mood</button>
</template>

<script>
import axios from "axios";
import VueApexCharts from "vue3-apexcharts";

export default {
  components: {
    apexchart: VueApexCharts,
  },
  data() {
    return {
      items: [],
      chartOptions: {
        dataLabels: {
          enabled: false,
        },
        colors: ["#008FFB"],
        xaxis: {
          type: "category",
        },
        title: {
          text: "HeatMap Chart (Single color)",
        },
      },
      series: [
        {
          name: "jan",
          data: this.generateData(31, {
            min: 1,
            max: 90,
          }),
        },
        {
          name: "feb",
          data: this.generateData(28, {
            min: 2,
            max: 90,
          }),
        },
        {
          name: "mar",
          data: this.generateData(31, {
            min: 2,
            max: 90,
          }),
        },
        {
          name: "apr",
          data: this.generateData(30, {
            min: 2,
            max: 90,
          }),
        },
      ],
    };
  },
  async created() {
    let result = await axios.get("http://localhost:4000/mood/all");
    this.items = result.data;
  },
  methods: {
    handleOnAdd() {
      this.$router.push("create");
    },
    generateData(count, yrange) {
      var i = 0;
      var series = [];
      while (i < count) {
        var x = (i + 1).toString();
        var y =
          Math.floor(Math.random() * (yrange.max - yrange.min + 1)) +
          yrange.min;
        series.push({
          x: x,
          y: y,
        });
        i++;
      }
      return series;
    },
  },
};
</script>

<style scoped></style>
