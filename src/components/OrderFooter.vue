<template>
  <div class="order-footer">
    <div class="body-header">确认订单</div>

    <div class="footer-body">
      <div class="demo-input">
        操作人：
        <el-input
          class="input-num"
          v-model="operator"
          placeholder="请输入内容"
          size="mini"
        ></el-input>
      </div>

      <div class="block">
        <span class="demonstration">操作日期：</span>
        <el-date-picker
          v-model="date"
          size="mini"
          type="date"
          placeholder="选择日期"
        >
        </el-date-picker>
      </div>
      <el-button @click="submit" class="btn" type="primary">提交订单</el-button>
    </div>
  </div>
</template>

<script>
import bus from "../bus";

export default {
  data() {
    return {
      operator: "",
      date: "",
      resData: {}
    };
  },
  methods: {
    submit() {
      let jsonRes = JSON.stringify(this.resData);
      alert(jsonRes);
    },
  },
  created() {
    bus.$on("bodyMessage", (rawData) => {
      this.resData = rawData;
    });
  }
};
</script>

<style scoped>
.order-footer {
  position: relative;
  margin-top: 20px;
  width: 100%;
  height: 100px;
  font-size: 12px;
  box-sizing: border-box;
  background: rgb(250, 248, 248);
  border: 1px solid rgb(173, 194, 196);
}
.order-footer .body-header {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  background: rgb(231, 230, 230);
  border-bottom: 1px solid rgb(173, 194, 196);
}
.footer-body {
  width: 100%;
  display: flex;
  padding: 15px;
}
.input-num {
  width: 180px;
}
.btn {
  position: absolute;
  right: 20px;
}
</style>