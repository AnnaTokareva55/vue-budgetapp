<template>
  <el-dialog title="Удалить из истории бюджета?" :visible.sync="dialogVisible" width="30%">
    <div class="list-item">
      <div>
        <i :class="iconClass" />
        <span class="budget-comment">{{listItemDel.comment}}</span>
      </div>
      <span class="budget-value" :class="textColorClass">{{listItemDel.value}}</span>
    </div>
    <span slot="footer" class="dialog-footer">
      <el-button @click="deleteCancel">Отмена</el-button>
      <el-button type="primary" @click="deleteItem(listItemDel.id)">Удалить</el-button>
    </span>
  </el-dialog>
</template>

<script>
export default {
  name: "DialogDeleteItem",
  props: {
    listItemDel: {
      type: Object,
      default: () => ({})
    },
    iconClass: {
      type: String,
      default: ""
    },
    textColorClass: {
      type: String,
      default: ""
    },
    dialogVisible: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
    deleteCancel() {
      this.$emit("deleteCancel");
    }
  }
};
</script>

<style scoped>
.list-item {
  display: flex;
  justify-content: space-evenly;
}
.budget-value {
  font-weight: bold;
}
</style>