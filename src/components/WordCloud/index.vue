<template>
  <div id="word-cloud-chart" :style="{ width: '100%', height: '100%' }"></div>
</template>

<script>
import "echarts-wordcloud";

export default {
  name: "WordCloud",
  data() {
    return {};
  },
  mounted() {
    const chartDom = document.getElementById("word-cloud-chart");
    const chart = this.$echarts.init(chartDom);
    chart.setOption({
      series: [
        {
          type: "wordCloud",
          shape: "circle",
          textStyle: {
            normal: {
              fontFamily: "sans-serif",
              fontWeight: "bold",
              // Color can be a callback function or a color string
              color: function() {
                // Random color
                return (
                  "rgb(" +
                  [
                    Math.round(Math.random() * 160),
                    Math.round(Math.random() * 160),
                    Math.round(Math.random() * 160)
                  ].join(",") +
                  ")"
                );
              }
            },
            emphasis: {
              shadowBlur: 10,
              shadowColor: "#333"
            }
          },
          data: [
            {
              name: "Vue",
              value: 366 * Math.random()
            },
            {
              name: "React",
              value: 326 * Math.random()
            },
            {
              name: "Webpack",
              value: 300 * Math.random()
            },
            {
              name: "Css3",
              value: 100 * Math.random()
            },
            {
              name: "可视化",
              value: 290 * Math.random()
            },
            {
              name: "微前端",
              value: 190 * Math.random()
            },
            {
              name: "WebGL",
              value: 247 * Math.random()
            },
            {
              name: "Canvas",
              value: 147 * Math.random()
            },
            {
              name: "前端监控",
              value: 290 * Math.random()
            },
            {
              name: "NodeJS",
              value: 310 * Math.random()
            },
            {
              name: "工程化",
              value: 270 * Math.random()
            }
          ]
        }
      ]
    });
  },
  methods: {}
};
</script>

<style lang="scss" scoped></style>
