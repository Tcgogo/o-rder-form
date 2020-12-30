<template>
  <div id="app">
    <header class="header">
      <h4>订单管理</h4>
    </header>
    <main class="main">
      <order-header></order-header>
      <order-body></order-body>
      <order-footer></order-footer>
    </main>
  </div>
</template>

<script>
import OrderHeader from "./components/OrderHeader";
import OrderBody from "./components/OrderBody";
import OrderFooter from "./components/OrderFooter";

export default {
  name: 'App',
  components: {
    OrderHeader,
    OrderBody,
    OrderFooter
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  position: relative;
  top: 0;
  left: 50%;
  margin-top: 60px;
  transform: translateX(-50%);
  width: 60vw;
  background: rgb(255, 255, 255);
  border-left: 1px solid rgb(173, 172, 172);
  border-top: 1px solid rgb(173, 172, 172);
  box-shadow: 2px 2px 3px rgb(116, 116, 116);
}

#app .header {
  width: 100%;
  height: 80px;
  background: rgb(240, 238, 238);
  display: flex;
  align-items: center;
  box-shadow: 0 2px 3px rgb(116, 116, 116);
}

.main {
  padding: 20px;
}

#app .header h4{
  margin-left: 20px;
  font-size: 20px;
}
.span-red {
  font-size: 20px;
  color: red;
}
</style>
