<template>
  <div id="app">
    <Form @submitForm="onFormSubmit" />
    <TotalBalance :total="totalBalance" />
    <BudgetList :list="list" @deleteItem="onDeleteItem" />
  </div>
</template>

<script>
import BudgetList from "@/components/BudgetList";
import TotalBalance from "@/components/TotalBalance";
import Form from "@/components/Form";

export default {
  name: "App",
  components: {
    BudgetList,
    TotalBalance,
    Form
  },
  data: () => ({
    list: {
      1: {
        type: "INCOME",
        value: 100000,
        comment: "Поступление зарплаты.",
        id: 1
      },
      2: {
        type: "OUTCOME",
        value: -5000,
        comment: "Оплата к/у.",
        id: 2
      }
    }
  }),
  computed: {
    /**
     * Расчет текущего баланса.
     */
    totalBalance() {
      return Object.values(this.list).reduce(
        (acc, item) => acc + item.value,
        0
      );
    }
  },
  methods: {
    /**
     * Удаление объекта из list.
     * @param {string} id - id объекта.
     */
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    /**
     * Добавление нового объекта в list.
     * @param {object} data - новый объект для добавления.
     */
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.$set(this.list, newObj.id, newObj);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.danger {
  color: #f56c6c;
}
.success {
  color: #67c23a;
}
</style>