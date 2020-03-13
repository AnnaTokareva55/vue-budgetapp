<template>
  <div class="list-item" v-if="typeFilter === listItem.type || typeFilter === 'ALL'">
    <i :class="iconClass" />
    <span class="budget-comment">{{listItem.comment}}</span>
    <span class="budget-value" :class="textColorClass">{{listItem.value}}</span>
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
    },
    typeFilter: {
      type: String,
      default: "ALL"
    }
  },
  computed: {
    textColorClass() {
      return this.listItem.type === "OUTCOME"
        ? "danger"
        : this.listItem.type === "INCOME"
        ? "success"
        : "";
    },
    iconClass() {
      return this.listItem.type === "OUTCOME"
        ? "el-icon-bottom-right danger"
        : this.listItem.type === "INCOME"
        ? "el-icon-top-right success"
        : "";
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
