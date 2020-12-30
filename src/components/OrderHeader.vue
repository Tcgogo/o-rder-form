<template>
  <div class="order-header">
    <div class="demo-input">
      订单号<span class="span-red">*</span>:
      <el-input
        class="input-num"
        v-model="orderNum"
        placeholder="请输入内容"
        size="mini"
      ></el-input>
    </div>

    <div class="demo-input">
      产品名称<span class="span-red">*</span>:
      <el-input
        class="input-num"
        v-model="productName"
        placeholder="请输入内容"
        size="mini"
      ></el-input>
    </div>

    <div class="demo-input">
      <div class="block">
        <span class="demonstration"
          >下单时间<span class="span-red">*</span></span
        >
        <el-date-picker
          size="mini"
          v-model="date"
          type="date"
          placeholder="选择日期"
        >
        </el-date-picker>
      </div>
    </div>
  </div>
</template>

<script>
import bus from "../bus";

export default {
  data() {
    return {
      orderNum: "",
      productName: "",
      date: "",
    };
  },
  created() {
    bus.$on("bodyMessage", (rawData) => {
      this.orderNum = rawData.orderNum;
      this.productName = rawData.productName;
    });
  },
  updated() {
    let rawData = {
      orderNum: this.orderNum,
      productName: this.productName,
      data: this.date
    };
    bus.$emit("headerMessage", rawData);
  },
};
</script>

<style scoped>
.order-header {
  display: flex;
  width: 100%;
  height: 80px;
  padding: 20px;
  box-sizing: border-box;
  background: rgb(231, 230, 230);
  font-size: 12px;
  border: 1px solid rgb(173, 194, 196);
}
.order-header .input-num {
  width: 100px;
  height: 20px;
  padding-right: 20px;
}
.span-symbol {
  margin-right: 15px;
}
</style>