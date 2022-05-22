<template>
  <div class="home">
    <ev-form
      ref="evForm"
      :form-data="formData"
      :form-config="formConfig"
      :rules="rules"
      :isShowData="isShowData"
    >
      <template #submitBtn>
        <el-button type="primary" @click="submit">立即创建</el-button>
      </template>
    </ev-form>
  </div>
</template>

<script>
// @ is an alias to /src
import EvForm from "@/base-ui/ev-form";
export default {
  name: "HomeView",
  components: {
    EvForm,
  },
  methods: {
    submit() {
      // 1. 表单校验
      this.$refs.evForm
        .submitForm()
        .then((val) => {
          console.log(this.formData);
          console.log("发请求了");
        })
        .catch((reason) => {
          console.log("不发请求");
        });
    },
  },
  created() {
    // setTimeout(() => {
    //   this.formData = {
    //     name: "1",
    //     region: "beijing",
    //   };
    //   this.isShowData = true
    // }, 1000);
  },
  data() {
    return {
      isShowData: false,
      formData: {
        name: "",
        region: "",
      },
      rules: {
        name: [
          { required: true, message: "请输入活动名称", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 3 到 5 个字符", trigger: "blur" },
        ],
        region: [
          { required: true, message: "请选择活动区域", trigger: "change" },
        ],
      },
      formConfig: [
        {
          filed: "name",
          label: "名称",
          type: "input",
        },
        {
          filed: "region",
          label: "活动区域",
          type: "select",
          selectOption: [
            {
              label: "选择一",
              value: "shanghai",
            },
            {
              label: "选择二",
              value: "beijing",
            },
          ],
        },
      ],
    };
  },
};
</script>
