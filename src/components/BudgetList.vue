<template>
  <div class="budget-list-wrap">
    <el-card :header="header">
      <FilterBudgetList @showFiltered="showFiltered" />
      <template v-if="!isEmpty">
        <BudgetListItem
          v-for="(listItem, prop) in list"
          :key="prop"
          :listItem="listItem"
          :typeFilter="typeFilter"
          @deleteItem="deleteItem"
        />
      </template>
      <template v-else>
        <el-alert :closable="false" :title="emptyList" type="info" />
      </template>
    </el-card>
  </div>
</template>

<script>
import FilterBudgetList from "@/components/FilterBudgetList";
import BudgetListItem from "@/components/BudgetListItem";

export default {
  name: "BudgetList",
  components: {
    FilterBudgetList,
    BudgetListItem
  },
  data: () => ({
    typeFilter: "ALL",
    header: "История бюджета",
    emptyList: "Список пуст."
  }),
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    isEmpty() {
      if (!Object.keys(this.list).length) return true;
      if (this.typeFilter !== "ALL") {
        const isFiltered = Object.values(this.list).find(
          item => item.type === this.typeFilter
        );
        return !isFiltered;
      } else return false;
    }
  },
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
    showFiltered(typeFilter) {
      this.typeFilter = typeFilter;
    }
  }
};
</script>

<style scoped>
.budget-list-wrap {
  max-width: 50%;
  margin: auto;
}
</style>