<template>
  <div class="root">
    <div class="list_item" v-for="(income, index) in incomeOps" :key="index">
      <div class="purchase_left">
        <h2 class="purchase_list">{{ income.source }}</h2>
        <p class="purchase_comment">Comment: {{ income.comment }}</p>
      </div>
      <div class="purchase_right">
        <p class="purchase_amount income">+{{ income.receivedAmount }}</p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "ItemIncomeList",
  props: ["incomeOps"],
  data() {
    return {};
  },
  methods: {},
};
</script>
<style scoped>
.root {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin: 0 auto;
}

.list_item {
  display: flex;
  flex-wrap: wrap;
  width: 98%;
  margin: 20px auto;
  justify-content: space-between;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
}

.purchase_left {
  width: 50%;
  padding: 10px;
}

.purchase_comment {
  color: rgb(80, 76, 76);
}

.purchase_right {
  display: flex;
  flex-wrap: wrap;
  width: 50%;
  padding: 10px;
  justify-content: right;
}

.purchase_right > p {
  font-size: 18px;
  margin: 10px 45px;
}

.purchase_amount {
  color: red;
}

.purchase_amount.income {
  color: rgb(26, 150, 26);
}

.purchase_right > p:last-child {
  font-weight: bolder;
  margin: 10px 50px;
}
</style>