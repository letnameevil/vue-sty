<template>
  <div class="ev-form">
    <el-form
      ref="evForm"
      :label-position="labelPosition"
      label-width="80px"
      :model="formData"
      :rules="rules"
    >
      <el-row :gutter="20">
        <template v-for="(item, index) in formConfig">
          <el-col :span="6" :key="index"
            ><el-form-item :label="item.label" :prop="item.filed">
              <el-input
                v-if="item.type === 'input'"
                v-model="formData[item.filed]"
                :disabled="isShowData"
              ></el-input>
              <el-select
                v-model="formData[item.filed]"
                placeholder="请选择活动区域"
                v-if="item.type === 'select'"
                :disabled="isShowData"
              >
                <el-option
                  v-for="optionItem in item.selectOption"
                  :key="optionItem.label"
                  :label="optionItem.label"
                  :value="optionItem.value"
                ></el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </template>
      </el-row>
      <div class="btn-container">
        <el-form-item>
          <slot name="submitBtn"></slot>
          <slot name="resetBtn"></slot>
        </el-form-item>
      </div>
    </el-form>
  </div>
</template>

<script>
export default {
  props: {
    formData: {
      type: Object,
      default: () => ({}),
    },
    formConfig: {
      type: Array,
      default: () => [],
    },
    rules: {
      type: Object,
      default: () => ({}),
    },
    isShowData: {
      type: Boolean,
      default: false,
    },
  },
  // watch: {
  //   formData(newValue, oldValue) {
  //     console.log(newValue, oldValue);
  //   },
  // },
  data() {
    return {
      labelPosition: "right",
    };
  },
  methods: {
    submitForm() {
      return new Promise((resolve, reject) => {
        this.$refs.evForm.validate((valid) => {
          if (valid) {
            resolve(true);
            console.log(123);
            return true;
          } else {
            reject(false);
            console.log(6666);
            return false;
          }
        });
      });
    },
    resetForm() {
      this.$refs.evForm.resetFields();
    },
  },
};
</script>

<style lang="less" scoped>
.btn-container {
  display: flex;
  justify-content: flex-end;
}
</style>
