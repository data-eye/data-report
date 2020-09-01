<template>
  <div
    id="fans-distributed-chart"
    :style="{ width: '100%', height: '100%' }"
  ></div>
</template>

<script>
import "echarts/extension/bmap/bmap";
import mapConfig from "../../assets/custom_map_config.json";
export default {
  name: "BMapScatter",
  data() {
    return {
      bmap: {}
    };
  },
  mounted() {
    const chartDom = document.getElementById("fans-distributed-chart");
    const chart = this.$echarts.init(chartDom);
    chart.setOption({
      bmap: {
        center: [104.114129, 37.550339],
        zoom: 5,
        roam: true,
        mapStyle: {
          styleJson: mapConfig
        }
      }
    });
    this.bmap = chart
      .getModel()
      .getComponent("bmap")
      .getBMap();
    this.bmap.setMapStyleV2({
      styleId: "8753450f45af88af2e68c5ee82e21928"
    });
  }
};
</script>
