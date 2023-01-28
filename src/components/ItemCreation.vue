<template>
  <div class="root">
    <div class="type">
      <select name="" id="itemType" v-model="itemType">
        <option v-for="(type, index) in types" :key="index">
          {{ type }}
        </option>
      </select>
      <div class="profit up" :balance="balance" v-if="balance > 0">
        Profit/Loss: +{{ balance }}
      </div>
      <div class="profit loss" :balance="balance" v-else-if="balance < 0">
        Profit/Loss: {{ balance }}
      </div>
      <div class="profit" :balance="balance" v-else-if="balance == 0 || balance == ''">
        Profit/Loss: 0
      </div>
    </div>
    <div class="main_top" v-if="itemType == 'Expense'">
      <div class="first">
        <input type="text" id="item_name" v-model="item_name" placeholder="What did you purchase?" />
        <select id="" v-model="item_category">
          <option v-for="(category, index) in categories" :key="index">
            {{ category }}
          </option>
        </select>
        <input type="date" name="" id="dateOfPurchase" v-model="item_purchasedate" />
      </div>
      <div class="second">
        <div class="block_cost">
          Cost:
          <input type="number" id="cost" v-model="item_cost" placeholder="How much did it cost?" />
        </div>
        <div class="block_comment">
          Comment:
          <input type="text" id="comment" v-model="item_comment" placeholder="Enter comment..." />
        </div>
        <div class="block_button">
          <button type="button" id="addBtn" @click="addToTheList">Add</button>
        </div>
      </div>
    </div>
    <div class="main_secondary_top" v-else>
      <div class="first">
        <input type="text" id="income_source" v-model="income_source" placeholder="Enter the source..." />
        <input type="number" id="income_title" v-model="income_amount" placeholder="Enter the amount..." />
        <input type="text" name="" id="income_comment" v-model="income_comment" placeholder="Enter comment..." />
        <button type="button" id="incomeBtn" @click="addSourceOfIncome">
          Add source of income
        </button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "ItemCreation",
  props: ["categories", "balance"],
  data() {
    return {
      item_name: "",
      item_category: "",
      item_purchasedate: "",
      item_cost: 1000,
      item_comment: "",
      types: ["Income", "Expense"],
      itemType: "",

      income_source: "",
      income_amount: "",
      income_comment: "",
    };
  },
  methods: {
    addToTheList() {
      if (
        this.item_name != "" &&
        this.item_category != "" &&
        this.item_purchasedate != "" &&
        this.item_cost >= 1 &&
        this.itemType == "Expense"
      ) {
        this.$emit("addToTheList", {
          type: this.itemType,
          name: this.item_name,
          category: this.item_category,
          purchasedate: this.item_purchasedate,
          cost: this.item_cost,
          comment: this.item_comment,
        });
      }
    },

    addSourceOfIncome() {
      if (
        this.income_source.length > 2 &&
        this.income_amount >= 1000 &&
        this.itemType == "Income"
      ) {
        this.$emit("addSourceOfIncome", {
          type: this.itemType,
          source: this.income_source,
          amount: this.income_amount,
          comment: this.income_comment,
        });
      }
    },
  },
};
</script>
<style scoped>
/* MAIN TOP STARTS */

.main_top {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  padding: 15px;
  margin: 20px auto;
  justify-content: space-between;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
}

.main_secondary_top {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  padding: 15px;
  margin: 20px auto;
  justify-content: space-between;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
}

.root {
  width: 100%;
}

.type {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin: 10px auto;
  justify-content: space-between;
}

.type>select {
  width: 15%;
  padding: 8px;
  border: none;
  outline: none;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 25px;
}

.profit {
  padding: 10px;
  font-size: 20px;
  font-weight: bolder;
}

.profit.up {
  color: rgb(26, 150, 26);
}

.profit.loss {
  color: red;
}

#income_title,
#income_source,
#income_comment {
  width: 25%;
  padding: 0 15px;
  border: none;
  outline: none;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 25px;
}

#incomeBtn {
  width: 20%;
  padding: 10px;
  border: none;
  outline: none;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
  font-weight: bold;
  cursor: pointer;
}

.first,
.second {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin: 0 auto;
  justify-content: space-between;
}

.second {
  padding: 20px 0;
}

.block_cost>input,
.block_comment>input {
  width: 75%;
  padding: 10px;
  border: none;
  outline: none;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 5px;
}

.block_cost {
  padding: 0 5px;
}

.block_cost,
.block_comment,
.block_button {
  width: 33%;
}

.block_button {
  display: flex;
  flex-wrap: wrap;
  justify-content: right;
}

#addBtn {
  width: 91%;
  padding: 10px;
  border: none;
  outline: none;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
  font-weight: bold;
  cursor: pointer;
}

#item_name {
  width: 60%;
  padding: 10px;
  border: none;
  outline: none;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
}

select {
  width: 10%;
  text-align: center;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
}

#dateOfPurchase {
  padding: 10px;
  border: none;
  outline: none;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
}

/* MAIN TOP ENDS */
</style>