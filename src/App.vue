<template>
  <div id="app">
    <div class="container">
      <div class="chart"></div>
      <hr />
      <div class="main">
        <ItemCreation
          :categories="categories"
          @addToTheList="fetchData($event)"
          @addSourceOfIncome="fetchIncomeData($event)"
          :balance="profit"
        />
        <div class="operations">
          <ItemExpensesList :expenses="expenses" />
          <ItemIncomeList :incomeOps="income" />
        </div>
        <FilteredItems
          :categories="categories"
          :expenses="filteredArray"
          :biggestExpenditure="biggestExpenditure"
          @filterAnArray="fetchFilteredData($event)"
          @biggestExpenditure="fetchBiggestSpendingsData($event)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ItemCreation from "./components/ItemCreation.vue";
import ItemExpensesList from "./components/ItemExpensesList.vue";
import ItemIncomeList from "./components/ItemIncomeList.vue";
import FilteredItems from "./components/FilteredItems.vue";

export default {
  name: "App",
  props: ["expensesOperations", "incomeOperations", "operationType"],
  emits: ["addToTheList", "addSourceOfIncome", "balance"],
  data() {
    return {
      result: {},
      incomeResult: {},
      expenses: [],
      income: [],
      filteredArray: [],
      categories: [
        "Food",
        "Housing",
        "Entertainment",
        "Healthcare",
        "Clothes",
        "Commuting",
        "Communication",
        "Other",
      ],
      currentDate: "",
      profit: 0,
      accumulated: 0,
      biggestExpenditure: [],
    };
  },

  components: {
    ItemCreation,
    ItemExpensesList,
    ItemIncomeList,
    FilteredItems,
  },

  methods: {
    fetchData(data) {
      this.result = data;
      this.currentDate = new Date(this.result.purchasedate);
      this.currentDate = `${
        this.currentDate.getMonth() + 1
      }/${this.currentDate.getDate()}/${this.currentDate.getFullYear()}`;

      if (this.result.type == "Expense") {
        this.expenses.push({
          type: this.result.type,
          items: this.result.name,
          category: this.result.category,
          date: this.currentDate,
          comment: this.result.comment,
          cost: this.result.cost,
        });
        this.profit -= parseInt(this.result.cost);
      }
    },

    fetchIncomeData(data) {
      this.result = data;
      if (this.result.type == "Income") {
        this.income.push({
          type: this.result.type,
          receivedAmount: this.result.amount,
          source: this.result.source,
          comment: this.result.comment,
        });
      }
      this.profit += parseInt(this.result.amount);
    },

    fetchFilteredData(data) {
      this.filteredArray = this.expenses.filter(
        (expense) => expense.category == data.category
      );
    },

    fetchBiggestSpendingsData() {
      this.expenses.forEach((element) => {
        this.accumulated += parseInt(element.cost);
      });

      this.biggestExpenditure = this.expenses.filter(
        (expense) =>
          parseInt(expense.cost) >
          parseInt(this.accumulated) / parseInt(this.expenses.length)
      );
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  margin: 60px 0;
}

.container {
  display: flex;
  flex-wrap: wrap;
  width: 75%;
  margin: 0 auto;
  border: 1px solid rgb(50, 135, 233);
  background-color: rgb(88, 86, 86);
  border-radius: 5px;
}

.chart {
  width: 95%;
  margin: 0 auto;
}

.main {
  display: flex;
  flex-wrap: wrap;
  width: 95%;
  margin: 0 auto;
}

.operations {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  margin: 10px auto;
  border: 1px solid rgb(50, 135, 233);
  border-radius: 8px;
}
</style>
