<template>
  <h3>Add New Transcation</h3>
  <form id="form" @submit.prevent="onsubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="enter text" v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - pexpense, positive - income)</label
      >
      <input
        type="number"
        id="amount"
        placeholder="enter amount"
        v-model="amount"
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>
<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";
const text = ref("");
const amount = ref("");
const toast = useToast();
const emit = defineEmits(["transactionsSubmitted"]);
const onsubmit = () => {
  if (!text.value || !amount.value) {
    toast.error("Both fields must be filled");
    return;
  }
  const transactionsData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };
  emit("transactionsSubmitted", transactionsData);
  text.value = "";
  amount.value = "";
};
</script>
