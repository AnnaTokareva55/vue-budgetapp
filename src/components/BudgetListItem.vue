<template>
  <div class="list-item">
    <i :class="getIconClass(listItem.type)" />
    <span class="budget-comment">{{listItem.comment}}</span>
    <span class="budget-value" :class="getTextColorClass(listItem.type)">{{listItem.value}}</span>
    <el-button type="danger" size="mini" @click="deleteDialogVisible(listItem)">Удалить</el-button>
    <DialogDeleteItem
      :listItemDel="listItemDel"
      :iconClass="iconClass"
      :textColorClass="textColorClass"
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
    iconClass: "",
    textColorClass: "",
    dialogVisible: false
  }),
  props: {
    listItem: {
      type: Object,
      default: () => ({})
    }
  },
  methods: {
    getIconClass(type) {
      return type === "OUTCOME"
        ? "el-icon-bottom-right danger"
        : type === "INCOME"
        ? "el-icon-top-right success"
        : "";
    },
    getTextColorClass(type) {
      return type === "OUTCOME" ? "danger" : type === "INCOME" ? "success" : "";
    },
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
    deleteCancel() {
      this.dialogVisible = false;
    },
    deleteDialogVisible(listItem) {
      this.listItemDel = { ...listItem };
      this.iconClass = this.getIconClass(listItem.type);
      this.textColorClass = this.getTextColorClass(listItem.type);
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
