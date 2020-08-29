<template>
  <common-card title="累计订单量" :value="orderToday">
    <template>
      <div
        id="total-orders-chart"
        :style="{ width: '100%', height: '100%' }"
      ></div>
    </template>
    <template v-slot:footer>
      <span>昨日订单量 </span>
      <span class="emphasis">{{ orderLastDay }}</span>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from "../../mixins/commonCardMixin";

export default {
  data() {
    return {
      orderToday: "320",
      orderLastDay: "80"
    };
  },
  mixins: [commonCardMixin],
  mounted() {
    const chartDom = document.getElementById("total-orders-chart");
    const chart = this.$echarts.init(chartDom);
    chart.setOption({
      xAxis: {
        type: "category",
        show: false,
        boundaryGap: false
      },
      yAxis: {
        show: false
      },
      series: [
        {
          type: "line",
          data: [350, 420, 540, 360, 340, 290, 510, 230, 310],
          areaStyle: {
            color: "purple"
          },
          lineStyle: {
            width: 0
          },
          itemStyle: {
            opacity: 0
          },
          smooth: true
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
