<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const toast = useToast();
const text = ref("");
const amount = ref("");

const emit = defineEmits(["addTransaction"]);

const onSubmit = () => {
  if (text.value === "" || amount.value === "") {
    return toast.error("Please fill in all fields");
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit("addTransaction", transactionData);
};
</script>

<template>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input v-model="text" type="text" id="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        v-model="amount"
        type="number"
        id="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button
      class="bg-zinc-900 text-white rounded-md px-4 py-3 border border-slate-100 mt-4 hover:bg-zinc-800 transition-all"
    >
      Add transaction
    </button>
  </form>
</template>
