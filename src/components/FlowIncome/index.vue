<template>
  <common-card title="流量收益" :value="salesToday">
    <template>
      <div class="compare-wrapper">
        <div class="compare">
          <span>日同比</span>
          <span class="emphasis">{{ salesGrowthLastDay }}</span>
          <div class="increase" />
        </div>
        <div class="compare">
          <span>月同比</span>
          <span class="emphasis">{{ salesGrowthLastMonth }}</span>
          <div class="decrease" />
        </div>
      </div>
    </template>
    <template v-slot:footer>
      <span>昨日收益</span>
      <span class="emphasis">{{ salesLastDay }}</span>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from "../../mixins/commonCardMixin";

export default {
  mixins: [commonCardMixin],
  data() {
    return {
      salesToday: "¥39,040",
      salesGrowthLastDay: "3.01%",
      salesGrowthLastMonth: "5.78%",
      salesLastDay: "¥18,400"
    };
  }
};
</script>

<style lang="scss" scoped>
.compare-wrapper {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;

  .compare {
    display: flex;
    align-items: center;
    font-size: 12px;
    margin-top: 3px;
    color: #666;
  }
}
</style>
