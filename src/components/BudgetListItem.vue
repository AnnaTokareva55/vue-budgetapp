<template>
  <div class="list-item" v-if="isShow">
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
    /**
     * Проверка соответствия типа элемента (доход/расход) типу выбранной фильтрации.
     */
    isShow() {
      return (
        this.typeFilter === this.listItem.type || this.typeFilter === "ALL"
      );
    },
    /**
     * Определение цвета текста с суммой дохода/расхода.
     */
    textColorClass() {
      return this.listItem.type === "OUTCOME"
        ? "danger"
        : this.listItem.type === "INCOME"
        ? "success"
        : "";
    },
    /**
     * Определение иконки элемента списка в истории бюджета.
     */
    iconClass() {
      return this.listItem.type === "OUTCOME"
        ? "el-icon-bottom-right danger"
        : this.listItem.type === "INCOME"
        ? "el-icon-top-right success"
        : "";
    }
  },
  methods: {
    /**
     * Событие клика по кнопке "Удалить"(передается в родительский компонент).
     * @param {strind} id - id элемента списка в истории бюджета.
     */
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
    /**
     * Отмена удаления и закрытие диалогового окна.
     */
    deleteCancel() {
      this.dialogVisible = false;
    },
    /**
     * Открытие диалогового окна для подтверждения удаления.
     */
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