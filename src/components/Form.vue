<template>
  <el-card class="form-card">
    <el-form ref="addItemForm" :model="formData" :rules="rules">
      <el-form-item label="Тип" label-position="top">
        <el-select
          class="select-type"
          v-model="formData.type"
          prop="type"
          placeholder="Выберите тип..."
        >
          <el-option label="Доход" value="INCOME"></el-option>
          <el-option label="Расход" value="OUTCOME"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="Комментарий" prop="comment">
        <el-input v-model="formData.comment"></el-input>
      </el-form-item>
      <el-form-item label="Сумма" prop="value">
        <el-input v-model.number="formData.value"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">Добавить</el-button>
      </el-form-item>
    </el-form>
  </el-card>
</template>

<script>
export default {
  name: "Form",
  data: () => {
    var validateSum = (rule, value, callback) => {
      if (typeof value !== "number") {
        callback(new Error("Необходимо ввести число."));
      } else if (value < 0) {
        callback(new Error("Сумма должна быть положительной."));
      } else if (value == 0) {
        callback(new Error("Необходимо ввести сумму."));
      } else callback();
    };
    return {
      formData: {
        type: "INCOME",
        comment: "",
        value: 0
      },
      rules: {
        type: [
          {
            required: true,
            message: "Необходимо выбрать тип данных.",
            trigger: "blur"
          }
        ],
        comment: [
          {
            required: true,
            message: "Необходимо добавить комментарий.",
            trigger: "blur"
          }
        ],
        value: [
          {
            validator: validateSum,
            trigger: "change"
          }
        ]
      }
    };
  },
  methods: {
    onSubmit() {
      console.log(111);
      this.$refs.addItemForm.validate(valid => {
        if (valid) {
          console.log(222);
          const type = this.formData.type;
          const coefficient =
            type === "INCOME" ? 1 : type === "OUTCOME" ? -1 : 0;
          this.$emit("submitForm", {
            ...this.formData,
            value: (this.formData.value *= coefficient)
          });
          this.$refs.addItemForm.resetFields();
        }
      });
    }
  }
};
</script>

<style scoped>
.form-card {
  max-width: 50%;
  margin: auto;
}
.select-type {
  width: 100%;
}
</style>