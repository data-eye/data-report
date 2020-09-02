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
      bmap: {},
      fansCommonCityPoint: [
        {
          name: "广州",
          value: [113.282065, 23.136399, 1800]
        },
        {
          name: "厦门",
          value: [118.131792, 24.483829, 1780]
        },
        {
          name: "郑州",
          value: [113.670798, 34.752965, 1500]
        },
        {
          name: "武汉",
          value: [114.310149, 30.604435, 1200]
        },
        {
          name: "西安",
          value: [108.943878, 34.346792, 1200]
        },
        {
          name: "长沙",
          value: [112.957256, 28.23489, 1000]
        },
        {
          name: "哈尔滨",
          value: [126.591341, 45.82209, 700]
        },
        {
          name: "长春",
          value: [125.333768, 43.863983, 730]
        }
      ],
      fansTopCityPoint: [
        {
          name: "北京",
          value: [116.433797, 39.910924, 2600]
        },
        {
          name: "上海",
          value: [121.484852, 31.237411, 2800]
        },
        {
          name: "深圳",
          value: [114.065414, 22.550058, 3200]
        },
        {
          name: "杭州",
          value: [120.188202, 30.271549, 2300]
        },
        {
          name: "南京",
          value: [114.310149, 30.604435, 2200]
        },
        {
          name: "成都",
          value: [104.070733, 30.672471, 2100]
        }
      ]
    };
  },
  mounted() {
    const chartDom = document.getElementById("fans-distributed-chart");
    const chart = this.$echarts.init(chartDom);
    chart.setOption({
      title: {
        text: "柯森全球粉丝分布",
        textStyle: {
          color: "#35635b",
          fontWeight: "bold",
          fontSize: 24
        },
        // subtext: "销售趋势统计",
        // sublink: "https://www.imooc.com",
        left: "center",
        top: 30
      },
      bmap: {
        center: [104.114129, 37.550339],
        zoom: 5,
        roam: true,
        mapStyle: {
          styleJson: mapConfig
        }
      },
      series: [
        {
          name: "CommonCity",
          type: "scatter",
          coordinateSystem: "bmap",
          data: this.fansCommonCityPoint,
          encode: {
            value: 2
          },
          // itemStyle: {
          //   color: 'purple'
          // },
          symbolSize: function(val) {
            return val[2] / 100;
          },
          label: {
            show: false,
            position: "right",
            formatter: function(v) {
              return `${v.data.name} - ${v.data.value[2]}`;
            }
          },
          // emphasis: {
          //   label: {
          //     show: true
          //   }
          // },
          itemStyle: {
            color: "#529471"
          }
        },
        {
          name: "TopCity",
          type: "effectScatter",
          coordinateSystem: "bmap",
          data: this.fansTopCityPoint,
          symbolSize: function(val) {
            return val[2] / 100;
          },
          encode: {
            value: 2
          },
          label: {
            formatter: function(v) {
              return `${v.data.name} - ${v.data.value[2]}`;
            },
            position: "right",
            show: false
          },
          hoverAnimation: true,
          rippleEffect: {
            brushType: "stroke"
          },
          itemStyle: {
            color: "#529471"
          }
        }
      ]
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
