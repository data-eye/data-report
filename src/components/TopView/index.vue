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
          <total-visitors />
        </el-card>
      </el-col>
      <el-col :span="6">
        <el-card shadow="hover">
          鼠标悬浮时显示
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import FlowIncome from "../FlowIncome";
import TotalOrder from "../TotalOrder";
import TotalVisitors from "../TotalVisitors";
export default {
  name: "TopView",
  components: {
    FlowIncome,
    TotalOrder,
    TotalVisitors
  }
};
</script>

<style></style>
