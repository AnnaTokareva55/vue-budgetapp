<template>
  <div class="filter">
    <!--<el-button type="success" plain @click="showIncomeOnly">Только доходы</el-button>
    <el-button type="danger" plain @click="showOutcomeOnly">Только расходы</el-button>
    <el-button type="primary" plain @click="showAll">Показать все</el-button>-->
    <el-button type="success" plain @click="showFiltered('INCOME')">Только доходы</el-button>
    <el-button type="danger" plain @click="showFiltered('OUTCOME')">Только расходы</el-button>
    <el-button type="primary" plain @click="showFiltered('ALL')">Показать все</el-button>
  </div>
</template>

<script>
export default {
  name: "FilterBudgetList",
  methods: {
    showFiltered(typeFilter) {
      this.$emit("showFiltered", typeFilter);
    }
  }
};
</script>

<style scoped>
</style>