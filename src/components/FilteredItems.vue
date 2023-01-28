<template>
  <div class="root">
    <div class="controls">
      <div class="controls_left">
        <select id="" v-model="chosen_category">
          <option v-for="(category, index) in categories" :key="index">
            {{ category }}
          </option>
        </select>
        <button type="button" @click="biggestSpendings" id="biggestSpendings">
          Biggest spendings
        </button>
      </div>
      <div class="controls_right">
        <button type="button" @click="filterAnArray" id="fltrBtn">
          Filter
        </button>
      </div>
    </div>
    <div class="output">
      <div
        class="output_item"
        v-for="(operation, index) in expenses"
        :key="index"
      >
        <div class="output_left">
          <h2 class="output_list">{{ operation.items }}</h2>
          <p class="output_comment">Comment: {{ operation.comment }}</p>
        </div>
        <div class="output_right">
          <p class="output_category">Category: {{ operation.category }}</p>
          <p class="output_date">Date: {{ operation.date }}</p>
          <p class="output_amount">-{{ operation.cost }}</p>
        </div>
      </div>
    </div>
    <div class="spendings">
      <div
        class="spendings_item"
        v-for="(expenditure, index) in biggestExpenditure"
        :key="index"
      >
        <div class="spendings_left">
          <h2 class="spendings_list">{{ expenditure.items }}</h2>
          <p class="spendings_comment">Comment: {{ expenditure.comment }}</p>
        </div>
        <div class="spendings_right">
          <p class="spendings_category">Category: {{ expenditure.category }}</p>
          <p class="spendings_date">Date: {{ expenditure.date }}</p>
          <p class="spendings_amount">-{{ expenditure.cost }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "FilteredItems",
  props: ["categories", "expenses", "biggestExpenditure"],
  data() {
    return {
      chosen_category: "",
    };
  },
  methods: {
    filterAnArray() {
      this.$emit("filterAnArray", {
        category: this.chosen_category,
      });
    },

    biggestSpendings() {
      this.$emit("biggestExpenditure", {
        emit: true,
      });
    },
  },
};
</script>
<style scoped>
.root {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin: 10px auto;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
}

.controls {
  display: flex;
  flex-wrap: wrap;
  width: 98%;
  margin: 10px auto 0 auto;
  padding: 10px;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
  justify-content: space-between;
}

.controls_left > select {
  width: 35%;
  padding: 8px;
  border: none;
  outline: none;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 25px;
  text-align: center;
}

.controls_left,
.controls_right {
  display: flex;
  flex-wrap: wrap;
  width: 50%;
}

.controls_left {
  justify-content: space-between;
}

.controls_right {
  justify-content: right;
}

#fltrBtn {
  width: 40%;
  padding: 10px;
  border: none;
  outline: none;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
  font-weight: bold;
  cursor: pointer;
}

#biggestSpendings {
  width: 45%;
  padding: 10px;
  border: none;
  outline: none;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
  font-weight: bold;
  cursor: pointer;
}

.output {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin: 0 auto;
}

.output_item {
  display: flex;
  flex-wrap: wrap;
  width: 98%;
  margin: 20px auto;
  justify-content: space-between;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
}

.output_left {
  width: 50%;
  padding: 10px;
}

.output_comment {
  color: rgb(80, 76, 76);
}

.output_right {
  display: flex;
  flex-wrap: wrap;
  width: 50%;
  padding: 10px;
  justify-content: right;
}

.output_right > p {
  font-size: 18px;
  margin: 10px 45px;
}

.output_amount {
  color: red;
}

.output_right > p:last-child {
  font-weight: bolder;
  margin: 10px 50px;
}

.spendings {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin: 0 auto;
}

.spendings_item {
  display: flex;
  flex-wrap: wrap;
  width: 98%;
  margin: 20px auto;
  justify-content: space-between;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
}

.spendings_left {
  width: 50%;
  padding: 10px;
}

.spendings_comment {
  color: rgb(80, 76, 76);
}

.spendings_right {
  display: flex;
  flex-wrap: wrap;
  width: 50%;
  padding: 10px;
  justify-content: right;
}

.spendings_right > p {
  font-size: 18px;
  margin: 10px 45px;
}

.spendings_amount {
  color: red;
}

.spendings_right > p:last-child {
  font-weight: bolder;
  margin: 10px 50px;
}
</style>