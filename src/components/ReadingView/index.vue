<template>
  <div class="sales-view">
    <el-card shadow="hover" :body-style="{ padding: '0 0 20px 0' }">
      <template v-slot:header>
        <div class="menu-wrapper">
          <el-menu
            :default-active="activeIndex"
            mode="horizontal"
            @select="onMenuSelect"
            class="sales-view-menu"
          >
            <el-menu-item index="1">阅读量</el-menu-item>
            <el-menu-item index="2">流量主收益</el-menu-item>
          </el-menu>
          <div class="menu-right">
            <el-radio-group v-model="radioSelect" size="small">
              <el-radio-button label="今日" />
              <el-radio-button label="本周" />
              <el-radio-button label="本月" />
              <el-radio-button label="今年" />
            </el-radio-group>
            <el-date-picker
              type="daterange"
              v-model="date"
              range-separator="至"
              start-placeholder="开始日期"
              end-placeholder="结束日期"
              size="small"
              unlink-panels
              :picker-options="pickerOptions"
              class="sales-view-date-picker"
            />
          </div>
        </div>
      </template>
      <template>
        <div class="sales-view-chart-wrapper">
          <!-- <v-chart :options="chartOption" /> -->
          <div class="echarts"></div>
          <div class="sales-view-list">
            <div class="sales-view-title">排行榜</div>
            <div class="list-item-wrapper">
              <div class="list-item" v-for="item in rankData" :key="item.id">
                <div :class="['list-item-id', +item.id <= 3 ? 'top-no' : '']">
                  {{ item.id }}
                </div>
                <div class="list-item-name">{{ item.name }}</div>
                <div class="list-item-reading">{{ item.reading }}</div>
              </div>
            </div>
          </div>
        </div>
      </template>
    </el-card>
  </div>
</template>

<script>
export default {
  name: "ReadingView",
  data() {
    return {
      activeIndex: "1",
      radioSelect: "今日",
      date: null,
      pickerOptions: {
        shortcuts: [
          {
            text: "最近一周",
            onClick(picker) {
              const start = new Date();
              const end = new Date();
              start.setTime(start.getTime() - 3600 * 24 * 1000 * 7);
              picker.$emit("pick", [start, end]);
            }
          },
          {
            text: "最近一个月",
            onClick(picker) {
              const start = new Date();
              const end = new Date();
              start.setTime(start.getTime() - 3600 * 24 * 1000 * 30);
              picker.$emit("pick", [start, end]);
            }
          },
          {
            text: "最近三个月",
            onClick(picker) {
              const start = new Date();
              const end = new Date();
              start.setTime(start.getTime() - 3600 * 24 * 1000 * 90);
              picker.$emit("pick", [start, end]);
            }
          }
        ]
      },
      orderRank: [],
      rankData: [
        {
          id: 1,
          name: "Chrome DevTools中的这些骚操作，你都知道吗？",
          reading: "932"
        },
        {
          id: 2,
          name: "你可能不知道的9条Webpack优化策略",
          reading: "820"
        },
        {
          id: 3,
          name: "从图片裁剪来聊聊前端二进制",
          reading: "802"
        },
        {
          id: 4,
          name: "聊一聊前端性能优化 CRP",
          reading: "790"
        },
        {
          id: 5,
          name: "那些前端开发必不可少的生产力工具",
          reading: "788"
        },
        {
          id: 6,
          name: "从 ElementUI 源码的构建流程来看前端 UI 库设计",
          reading: "709"
        }
      ],
      chartOption: {}
    };
  },
  computed: {
    // rankData() {
    //   return this.activeIndex === "1" ? this.orderRank : this.userRank;
    // }
  },
  methods: {
    onMenuSelect(index) {
      this.activeIndex = index;
      // if (index === '1') {
      //   this.render(this.orderFullYear, this.orderFullYearAxis, '年度销售额')
      // } else {
      //   this.render(this.userFullYear, this.userFullYearAxis, '年度用户访问量')
      // }
    }
  }
};
</script>

<style lang="scss" scoped>
.sales-view {
  margin-top: 20px;

  .menu-wrapper {
    position: relative;
    display: flex;

    .sales-view-menu {
      width: 100%;
      padding-left: 20px;

      .el-menu-item {
        height: 50px;
        line-height: 50px;
        margin: 0 20px;
      }
    }

    .menu-right {
      position: absolute;
      top: 0;
      right: 20px;
      height: 50px;
      display: flex;
      align-items: center;
      justify-content: flex-end;

      .sales-view-date-picker {
        margin-left: 20px;
      }
    }
  }

  .sales-view-chart-wrapper {
    display: flex;
    height: 270px;

    .echarts {
      flex: 0 0 70%;
      width: 70%;
      height: 100%;
    }

    .sales-view-list {
      flex: 1;
      width: 100%;
      height: 100%;
      overflow: hidden;

      .sales-view-title {
        margin-top: 20px;
        font-size: 12px;
        color: #666;
        font-weight: 500;
      }

      .list-item-wrapper {
        margin-top: 15px;

        .list-item {
          display: flex;
          align-items: center;
          font-size: 12px;
          height: 20px;
          padding: 6px 20px 6px 0;

          .list-item-id {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 20px;
            height: 20px;
            color: #333;

            &.top-no {
              background: #000;
              border-radius: 50%;
              color: #fff;
              font-weight: 500;
            }
          }

          .list-item-name {
            margin-left: 10px;
            color: #333;
          }

          .list-item-reading {
            flex: 1;
            text-align: right;
          }
        }
      }
    }
  }
}
</style>
