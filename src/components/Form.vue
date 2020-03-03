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
          <el-option label="Приход" value="INCOME"></el-option>
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
  data: () => ({
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
          required: true,
          message: "Необходимо ввести сумму.",
          trigger: "change"
        },
        {
          required: true,
          message: "Необходимо ввести число.",
          trigger: "change"
        }
      ]
    }
  }),
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate(valid => {
        if (valid) {
          this.$emit("submitForm", { ...this.formData });
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