<template>
  <div class="budget-list-wrap">
    <el-card :header="header">
      <template v-if="!isEmpty">
        <BudgetListItem
          v-for="(listItem, prop) in list"
          :key="prop"
          :listItem="listItem"
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
import BudgetListItem from "@/components/BudgetListItem";

export default {
  name: "BudgetList",
  components: {
    BudgetListItem
  },
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    header: "История бюджета",
    emptyList: "Список пуст."
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    }
  },
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
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