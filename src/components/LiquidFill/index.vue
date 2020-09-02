/* eslint-disable no-unreachable */
<template>
  <div id="liquid-fill-chart" :style="{ width: '100%', height: '100%' }"></div>
</template>

<script>
import "echarts-liquidfill";

export default {
  name: "LiquidFill",
  data() {
    return {};
  },
  mounted() {
    const chartDom = document.getElementById("liquid-fill-chart");
    const chart = this.$echarts.init(chartDom);
    chart.setOption({
      series: [
        {
          type: "liquidFill",
          data: [0.623],
          radius: "80%",
          label: {
            // formatter: v => {
            //   console.log("v", v);
            //   return `${(v.data * 100).toFixed(2)}%`;
            // },
            textStyle: {
              fontSize: 36,
              color: "#999",
              fontWeight: "normal"
            },
            position: ["50%", "50%"],
            insideColor: "#fff"
          },
          outline: {
            itemStyle: {
              borderColor: "#aaa4a4",
              borderWidth: 1,
              color: "none",
              shadowBlur: 0,
              shadowColor: "#fff"
            },
            borderDistance: 0
          },
          backgroundStyle: {
            color: "#bcd3c2"
          },
          itemStyle: {
            shadowBlur: 0,
            shadowColor: "#fff"
          },
          amplitude: 8,
          color: ["#6bba62"]
        }
      ]
    });
  },
  methods: {
    getColor(value) {
      if (value > 0 && value <= 0.5) {
        return "rgba(97,216,0,.7)";
      } else if (value > 0.5 && value <= 0.8) {
        return "rgba(204,178,26,.7)";
      } else if (value > 0.8) {
        return "rgba(241,47,28,.7)";
      }
      return "#c7c7cb";
    }
  }
};
</script>

<style lang="scss" scoped></style>
