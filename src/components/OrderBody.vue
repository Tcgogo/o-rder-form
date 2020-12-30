<template>
  <div class="order-body">
    <div class="body-header">订单信息</div>

    <div class="order-body-item">
      <div class="message-left">
        <div class="demo-input">
          订单号<span class="span-red">*</span>：
          <el-input
            class="input-num"
            v-model="orderNum"
            placeholder="请输入内容"
            size="mini"
          ></el-input>
        </div>

        <div class="demo-input">
          产品名称<span class="span-red">*</span>：
          <el-input
            class="input-num"
            v-model="productName"
            placeholder="请输入内容"
            size="mini"
          ></el-input>
        </div>

        <div class="demo-input">
          买家名称：
          <el-input
            class="input-num"
            v-model="buyerName"
            placeholder="请输入内容"
            size="mini"
          ></el-input>
        </div>

        <div class="demo-input">
          订单状态：
          <el-select
            class="input-num"
            size="mini"
            v-model="orderStatus"
            placeholder="请选择"
          >
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </div>

        <div class="demo-input">
          订单备注：
          <el-input
            class="input-num"
            v-model="orderRemark"
            placeholder="请输入内容"
            size="mini"
          ></el-input>
        </div>
      </div>

      <div class="message-right">
        <div class="demo-input">
          产品总价(￥)<span class="span-red">*</span>：
          <el-input
            class="input-num"
            v-model="productPrice"
            placeholder="请输入内容"
            size="mini"
          ></el-input>
        </div>

        <div class="demo-input">
          总重量(kg)：
          <el-input
            class="input-num"
            v-model="totalWeight"
            placeholder="请输入内容"
            size="mini"
          ></el-input>
        </div>

        <div class="demo-input">
          运费(￥)<span class="span-red">*</span>：
          <el-input
            class="input-num"
            v-model="freight"
            placeholder="请输入内容"
            size="mini"
          ></el-input>
        </div>

        <div class="demo-input">
          手续费(￥)：
          <el-input
            class="input-num"
            v-model="serviceCharge"
            placeholder="请输入内容"
            size="mini"
          ></el-input>
        </div>

        <div class="demo-input">
          附加费(￥)：
          <el-input
            class="input-num"
            v-model="otherPrice"
            placeholder="请输入内容"
            size="mini"
          ></el-input>
        </div>
      </div>
    </div>
    <div class="order-rental">
      订单总额: <span>{{ totalPrice }}</span>
    </div>
  </div>
</template>

<script>
import bus from "../bus";
export default {
  data() {
    return {
      options: [
        {
          value: "选项1",
          label: "未完成",
        },
        {
          value: "选项2",
          label: "已完成",
        },
        {
          value: "选项3",
          label: "未付款",
        },
        {
          value: "选项4",
          label: "错误订单",
        },
      ],
      orderNum: "",
      productName: "",
      buyerName: "",
      orderStatus: "",
      orderRemark: "",
      productPrice: 0,
      totalWeight: 0,
      freight: 0,
      serviceCharge: 0,
      otherPrice: 0,
    };
  },
  computed: {
    totalPrice() {
      let price =
        Number(this.productPrice) +
        Number(this.freight) +
        Number(this.serviceCharge) +
        Number(this.otherPrice);
      if (isNaN(price)) {
        return "金额请输入数值";
      } else {
        return price + "￥";
      }
    },
  },
  created() {
    bus.$on("headerMessage", (rawData) => {
      this.orderNum = rawData.orderNum;
      this.productName = rawData.productName;
    });
  },
  updated() {
    let rawData = {
      orderNum: this.orderNum,
      productName: this.productName,
      data: this.date,
      buyerName: this.buyerName,
      orderStatus: this.orderStatus,
      orderRemark: this.orderRemark,
      productPrice: this.productPrice,
      totalWeight: this.totalWeight,
      freight: this.freight,
      serviceCharge: this.serviceCharge,
      otherPrice: this.otherPrice,
    };
    bus.$emit("bodyMessage", rawData);
  },
};
</script>

<style scoped>
.order-body {
  position: relative;
  margin-top: 20px;
  width: 100%;
  font-size: 12px;
  box-sizing: border-box;
  background: rgb(250, 248, 248);
  border: 1px solid rgb(173, 194, 196);
}
.order-body .body-header {
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  background: rgb(231, 230, 230);
  border-bottom: 1px solid rgb(173, 194, 196);
}

.order-body-item {
  display: flex;
  justify-content: space-evenly;
}
.demo-input {
  margin: 10px 0;
  display: flex;
  justify-content: space-between;
}
.input-num {
  width: 180px;
}

.order-rental {
  font-size: 30px;
  margin: 20px;
}

.order-rental span {
  color: red;
}
</style>