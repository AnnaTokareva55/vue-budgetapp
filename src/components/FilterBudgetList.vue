<template>
  <div class="filter">
    <el-button type="success" plain @click="showFiltered('INCOME')">Только доходы</el-button>
    <el-button type="danger" plain @click="showFiltered('OUTCOME')">Только расходы</el-button>
    <el-button type="primary" plain @click="showFiltered('ALL')">Показать все</el-button>
  </div>
</template>

<script>
export default {
  name: "FilterBudgetList",
  methods: {
    /**
     * Событие по клику кнопки фильтрации (передается в родительский компонент).
     * @param {string} typeFilter - тип фильтрации.
     */
    showFiltered(typeFilter) {
      this.$emit("showFiltered", typeFilter);
    }
  }
};
</script>