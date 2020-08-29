<template>
  <common-card title="访客总人数" :value="totalVisitor">
    <template>
      <div
        id="today-users-chart"
        :style="{ width: '100%', height: '100%' }"
      ></div>
    </template>
    <template v-slot:footer>
      <span>昨日访客数</span>
      <span class="emphasis">{{ visitorLastDay }}</span>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from "../../mixins/commonCardMixin";

export default {
  data() {
    return {
      totalVisitor: "5200",
      visitorLastDay: "360"
    };
  },
  mixins: [commonCardMixin],
  mounted() {
    const chartDom = document.getElementById("today-users-chart");
    const chart = this.$echarts.init(chartDom);
    chart.setOption({
      color: ["#3398DB"],
      xAxis: {
        type: "category",
        data: ["06:00", "09:00", "12:00", "15:00", "18:00", "21:00", "24:00"]
      },
      yAxis: {
        show: false
      },
      series: [
        {
          type: "bar",
          data: [20, 30, 29, 15, 29, 50, 38],
          barWidth: "60%"
        }
      ],
      grid: {
        left: 0,
        top: 0,
        right: 0,
        bottom: 0
      }
    });
  },
  methods: {}
};
</script>
