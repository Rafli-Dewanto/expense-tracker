<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionLists from "./components/TransactionLists.vue";
import AddTransaction from "./components/AddTransaction.vue";
import { ref, computed, onMounted } from "vue";
import { useToast } from "vue-toastification";

const toast = useToast();

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));
  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

const total = computed(() =>
  transactions.value.reduce((acc, curr) => acc + curr.amount, 0)
);

const income = computed(() => {
  return transactions.value
    .filter((t) => t.amount > 0)
    .reduce((acc, curr) => acc + curr.amount, 0)
    .toFixed(2);
});

const expense = computed(() => {
  return transactions.value
    .filter((t) => t.amount < 0)
    .reduce((acc, curr) => acc + curr.amount, 0)
    .toFixed(2);
});

const handleAddTransaction = (newTransaction) => {
  transactions.value.push({
    id: Date.now(),
    ...newTransaction,
  });

  saveTransactionsToLocalStorage();

  text.value = "";
  amount.value = "";

  toast.success("Transaction added successfully");
};

const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};

const handleDeleteTransaction = (id) => {
  transactions.value = transactions.value.filter((t) => t.id !== id);
  toast.success("Transaction deleted successfully");
};
</script>

<template>
  <main class="grid grid-cols-1 place-items-center my-16">
    <Header />
    <div class="container my-6 max-w-[42rem] flex gap-x-24">
      <section class="space-y-6">
        <Balance :total="total" />
        <IncomeExpense :income="+income" :expense="+expense" />
        <TransactionLists
          :transactions="transactions"
          @deleteTransaction="handleDeleteTransaction"
        />
      </section>
      <AddTransaction @addTransaction="handleAddTransaction" />
    </div>
  </main>
</template>
