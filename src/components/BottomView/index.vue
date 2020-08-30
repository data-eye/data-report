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
        <!-- <template v-slot:header>
          <div class="title-wrapper">
            <div class="title">分类销售排行</div>
            <div class="radio-wrapper">
              <el-radio-group
                v-model="radioSelect"
                size="small"
                @change="onCategoryChange"
              >
                <el-radio-button label="品类"></el-radio-button>
                <el-radio-button label="商品"></el-radio-button>
              </el-radio-group>
            </div>
          </div>
        </template>
        <template>
          <div class="chart-wrapper">
            <v-chart :options="categoryOptions" />
          </div>
        </template> -->
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
      searchCount: 6000
      // radioSelect: '品类',
      // categoryOptions: {}
    };
  },
  mounted() {
    const chartUserDom = document.getElementById("total-search-user-chart");
    const chartUser = this.$echarts.init(chartUserDom);
    chartUser.setOption(this.searchUserOption);

    const chartCountDom = document.getElementById("total-search-count-chart");
    const chartCount = this.$echarts.init(chartCountDom);
    chartCount.setOption(this.searchCountOption);
  },
  methods: {
    onPageChange(page) {}
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
