<template>
  <div class="total-value" :class="textColorClass">Текущий баланс: {{total}}</div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0
    }
  },
  computed: {
    textColorClass() {
      return this.total < 0 ? "danger" : this.total > 0 ? "success" : "";
    }
  }
};
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}

.danger {
  color: #f56c6c;
}

.success {
  color: #67c23a;
}
</style>