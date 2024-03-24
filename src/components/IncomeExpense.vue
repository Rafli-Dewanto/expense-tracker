<script setup>
import { defineProps } from "vue";

const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expense: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <div class="flex justify-start bg-white py-4 space-x-8 px-4 rounded-md">
    <div>
      <h4 class="text-gray-700 font-semibold">Income</h4>
      <p id="money-plus" class="text-green-500 font-semibold">+${{ income }}</p>
    </div>
    <div>
      <h4 class="text-gray-700 font-semibold">Expense</h4>
      <p id="money-minus" class="text-red-500 font-semibold">-${{ expense }}</p>
    </div>
  </div>
</template>
