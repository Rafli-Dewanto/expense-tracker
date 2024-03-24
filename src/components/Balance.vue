<script setup>
import { defineProps } from "vue";

defineProps({
  total: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <h4 class="capitalize font-bold text-2xl">your balance</h4>
  <h1 id="balance" class="text-3xl">${{ total }}</h1>
</template>
