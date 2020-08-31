<template>
  <div class="bottom-view">
    <div class="view">
      <el-card shadow="hover">
        <template v-slot:header>
          <div class="title-wrapper">关键词搜索</div>
        </template>
        <template>
          <div class="chart-wrapper">
            <div class="chart-inner">
              <div class="chart">
                <div class="chart-title">搜索用户数</div>
                <div class="chart-data">{{ userCount }}</div>
                <div
                  id="total-search-user-chart"
                  :style="{ width: '100%' }"
                ></div>
              </div>
              <div class="chart">
                <div class="chart-title">搜索量</div>
                <div class="chart-data">{{ searchCount }}</div>
                <div
                  id="total-search-count-chart"
                  :style="{ width: '100%' }"
                ></div>
                <!-- <v-chart :options="searchNumberOption" /> -->
              </div>
            </div>
            <div class="table-wrapper">
              <el-table :data="tableData">
                <el-table-column prop="rank" label="排名" />
                <el-table-column prop="keyword" label="关键词" />
                <el-table-column prop="count" label="总搜索量" />
                <el-table-column prop="users" label="搜索用户数" />
                <el-table-column prop="range" label="搜索占比" />
              </el-table>
              <el-pagination
                layout="prev, pager, next"
                :total="total"
                :page-size="pageSize"
                background
                @current-change="onPageChange"
              ></el-pagination>
            </div>
          </div>
        </template>
      </el-card>
    </div>
    <div class="view">
      <el-card shadow="hover">
        <template v-slot:header>
          <div class="title-wrapper">
            <div class="title">文章分类</div>
            <div class="radio-wrapper">
              <el-radio-group
                v-model="radioSelect"
                size="small"
                @change="onCategoryChange"
              >
                <el-radio-button label="类型"></el-radio-button>
                <el-radio-button label="专辑"></el-radio-button>
              </el-radio-group>
            </div>
          </div>
        </template>
        <template>
          <div class="chart-wrapper">
            <!-- <v-chart :options="categoryOptions" /> -->
            <div
              id="total-category-chart"
              :style="{ width: '100%', height: '100%' }"
            ></div>
          </div>
        </template>
      </el-card>
    </div>
  </div>
</template>

<script>
export default {
  name: "BottomView",
  data() {
    return {
      searchUserOption: {
        xAxis: {
          type: "category",
          boundaryGap: false
        },
        yAxis: {
          show: false
        },
        tooltip: {},
        series: [
          {
            type: "line",
            data: [100, 150, 200, 250, 200, 150, 100, 50, 100, 150],

            areaStyle: {
              color: "rgba(95,187,255,.5)"
            },
            lineStyle: {
              color: "rgb(95,187,255)"
            },
            itemStyle: {
              opacity: 0
            },
            smooth: true
          }
        ],
        grid: {
          top: 0,
          left: 0,
          bottom: 0,
          right: 0
        }
      },
      searchCountOption: {
        xAxis: {
          type: "category",
          boundaryGap: false
        },
        yAxis: {
          show: false
        },
        tooltip: {},
        series: [
          {
            type: "line",
            data: [400, 550, 500, 450, 700, 550, 380, 350, 200, 850],

            areaStyle: {
              color: "rgba(95,187,255,.5)"
            },
            lineStyle: {
              color: "rgb(95,187,255)"
            },
            itemStyle: {
              opacity: 0
            },
            smooth: true
          }
        ],
        grid: {
          top: 0,
          left: 0,
          bottom: 0,
          right: 0
        }
      },
      tableData: [
        {
          id: 1,
          rank: 1,
          keyword: "Vue",
          count: 2210,
          users: 800,
          range: "30%"
        },
        {
          id: 2,
          rank: 2,
          keyword: "React",
          count: 1920,
          users: 700,
          range: "25%"
        },
        {
          id: 3,
          rank: 3,
          keyword: "浏览器",
          count: 1710,
          users: 500,
          range: "20%"
        },
        {
          id: 4,
          rank: 4,
          keyword: "NodeJS",
          count: 1600,
          users: 800,
          range: "20%"
        },
        {
          id: 5,
          rank: 5,
          keyword: "Webpack",
          count: 1502,
          users: 1000,
          range: "20%"
        },
        {
          id: 6,
          rank: 6,
          keyword: "技巧",
          count: 1200,
          users: 500,
          range: "10%"
        }
      ],
      totalData: [],
      total: 6,
      pageSize: 4,
      userCount: 1800,
      searchCount: 6000,
      radioSelect: "类型",
      categoryOptions: {}
    };
  },
  mounted() {
    const chartUserDom = document.getElementById("total-search-user-chart");
    const chartUser = this.$echarts.init(chartUserDom);
    chartUser.setOption(this.searchUserOption);

    const chartCountDom = document.getElementById("total-search-count-chart");
    const chartCount = this.$echarts.init(chartCountDom);
    chartCount.setOption(this.searchCountOption);

    this.renderPieChart();
  },
  methods: {
    onPageChange(page) {},
    renderPieChart() {
      const chartData = [
        {
          legendname: "源码",
          value: 13,
          percent: "45.5%",
          itemStyle: {
            color: "#515070"
          },
          name: "源码 | 45.5%"
        },
        {
          legendname: "骚操作/技巧",
          value: 2,
          percent: "7%",
          itemStyle: {
            color: "#43658b"
          },
          name: "骚操作/技巧 | 7%"
        },
        {
          legendname: "面试",
          value: 2,
          percent: "7%",
          itemStyle: {
            color: "#ed6663"
          },
          name: "面试 | 7%"
        },
        {
          legendname: "Chrome",
          value: 1,
          percent: "3.5%",
          itemStyle: {
            color: "#decdc3"
          },
          name: "Chrome | 3.5%"
        },
        {
          legendname: "React",
          value: 1,
          percent: "3.5%",
          itemStyle: {
            color: "#2d4059"
          },
          name: "React | 3.5%"
        },
        {
          legendname: "Vue",
          value: 5,
          percent: "17.5%",
          itemStyle: {
            color: "#ff8e6e"
          },
          name: "Vue | 17.5%"
        },
        {
          legendname: "数据结构与算法",
          value: 1,
          percent: "3.5%",
          itemStyle: {
            color: "#ffa372"
          },
          name: "数据结构与算法 | 3.5%"
        }
      ];
      this.categoryOptions = {
        title: [
          {
            text: `${this.radioSelect}分布`,
            textStyle: {
              fontSize: 14,
              color: "#666"
            },
            left: 20,
            top: 20
          },
          {
            text: "全部分类",
            subtext: "320",
            x: "34.5%",
            y: "42.5%",
            textStyle: {
              fontSize: 14,
              color: "#999"
            },
            subtextStyle: {
              fontSize: 28,
              color: "#333"
            },
            textAlign: "center"
          }
        ],
        series: [
          {
            name: "文章分类",
            type: "pie",
            data: chartData,
            label: {
              normal: {
                show: true,
                position: "outter",
                formatter: function(params) {
                  return params.data.legendname;
                }
              }
            },
            center: ["35%", "50%"],
            radius: ["45%", "60%"],
            labelLine: {
              normal: {
                length: 5,
                length2: 3,
                smooth: true
              }
            },
            clockwise: false,
            itemStyle: {
              borderWidth: 4,
              borderColor: "#fff"
            }
          }
        ],
        legend: {
          type: "scroll",
          orient: "vertical",
          height: 250,
          left: "70%",
          top: "middle",
          textStyle: {
            color: "#8c8c8c"
          }
        },
        tooltip: {
          trigger: "item",
          formatter: function(params) {
            console.log("toottip params", params);
            const str =
              params.seriesName +
              "<br />" +
              params.marker +
              params.data.legendname +
              "<br />" +
              "数量：" +
              params.data.value +
              "<br />" +
              "占比：" +
              params.data.percent +
              "%";
            return str;
          }
        }
      };
      const chartCategoryDom = document.getElementById("total-category-chart");
      const chartCategory = this.$echarts.init(chartCategoryDom);
      chartCategory.setOption(this.categoryOptions);
    },
    onCategoryChange(type) {
      this.radioSelect = type;
      this.renderPieChart();
    }
  }
};
</script>

<style lang="scss" scoped>
.bottom-view {
  display: flex;
  margin-top: 20px;

  .view {
    flex: 1;
    width: 50%;
    box-sizing: border-box;

    &:first-child {
      padding: 0 10px 0 0;
    }

    &:last-child {
      padding: 0 0 0 10px;
    }

    .title-wrapper {
      display: flex;
      align-items: center;
      height: 60px;
      box-sizing: border-box;
      border-bottom: 1px solid #eee;
      font-size: 14px;
      font-weight: 500;
      padding: 0 0 0 20px;

      .radio-wrapper {
        flex: 1;
        display: flex;
        justify-content: flex-end;
        padding-right: 20px;
      }
    }

    .chart-wrapper {
      display: flex;
      flex-direction: column;
      height: 452px;

      .chart-inner {
        display: flex;
        padding: 0 10px;
        margin-top: 20px;

        .chart {
          flex: 1;
          padding: 0 10px;

          .chart-title {
            color: #999;
            font-size: 14px;
          }

          .chart-data {
            font-size: 22px;
            color: #333;
            font-weight: 500;
            letter-spacing: 2px;
          }

          #total-search-user-chart,
          #total-search-count-chart {
            height: 50px;
          }
        }
      }

      .table-wrapper {
        flex: 1;
        margin-top: 20px;
        padding: 0 20px 20px;

        .el-pagination {
          display: flex;
          justify-content: flex-end;
          margin-top: 15px;
        }
      }
    }
  }
}
</style>
