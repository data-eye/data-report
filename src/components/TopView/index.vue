<template>
  <div>
    <el-row :gutter="20">
      <el-col :span="6">
        <el-card shadow="hover">
          <flow-income />
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card shadow="hover">
          <total-order />
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card shadow="hover">
          <today-visitors />
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card shadow="hover">
          <total-fans />
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import FlowIncome from "../FlowIncome";
import TotalOrder from "../TotalOrder";
import TodayVisitors from "../TodayVisitors";
import TotalFans from "../TotalFans";
export default {
  name: "TopView",
  components: {
    FlowIncome,
    TotalOrder,
    TodayVisitors,
    TotalFans
  }
};
</script>

<style></style>
