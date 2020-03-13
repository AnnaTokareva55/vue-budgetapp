<template>
  <div class="list-item">
    <span class="budget-comment">{{listItem.comment}}</span>
    <span class="budget-value">{{listItem.value}}</span>
    <el-button type="danger" size="mini" @click="deleteDialogVisible(listItem)">Удалить</el-button>
    <DialogDeleteItem
      :listItemDel="listItemDel"
      :dialogVisible="dialogVisible"
      @deleteItem="deleteItem"
      @deleteCancel="deleteCancel"
    />
  </div>
</template>

<script>
import DialogDeleteItem from "./DialogDeleteItem";

export default {
  name: "BudgetListItem",
  components: {
    DialogDeleteItem
  },
  data: () => ({
    listItemDel: {},
    dialogVisible: false
  }),
  props: {
    listItem: {
      type: Object,
      default: () => ({})
    }
  },
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
    deleteCancel() {
      this.dialogVisible = false;
    },
    deleteDialogVisible(listItem) {
      this.listItemDel = { ...listItem };
      this.dialogVisible = true;
    }
  }
};
</script>

<style scoped>
.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}
.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
</style>
