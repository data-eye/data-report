<template>
  <common-card title="今日访客总人数" :value="todayTotalVisitor">
    <template>
      <div
        id="today-visitors-chart"
        :style="{ width: '100%', height: '100%' }"
      ></div>
    </template>
    <template v-slot:footer>
      <span>取关人数</span>
      <span class="emphasis">{{ unsubscribeVisitor }}</span>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from "../../mixins/commonCardMixin";

export default {
  data() {
    return {
      todayTotalVisitor: "520",
      unsubscribeVisitor: 2
    };
  },
  mixins: [commonCardMixin],
  mounted() {
    const chartDom = document.getElementById("today-visitors-chart");
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
