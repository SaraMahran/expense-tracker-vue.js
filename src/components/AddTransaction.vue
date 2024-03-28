<template>
  <h3>Add New Transaction</h3>
  <form id="form" @submit.prevent="onSumbit">
    <div class="form-control">
      <label for="text">Type of transaction</label>
      <br />
      <input type="text" id="text" v-model="text" placeholder="Enter text here...">
    </div>
    <div class="form-control">
      <label for="amount">Amount <br />(Negative - expense, Positive - income)</label>
      <br />
      <input type="text" id="amount" v-model="amount" placeholder="Enter amount here...">
    </div>
    <button class="btn">Add Transation</button>
  </form>
</template>

<script setup>
import {ref} from 'vue';
import {useToast} from 'vue-toastification';

const text = ref('');
const amount = ref('');

const emit = defineEmits(['transactionSubmitted']);

const toast = useToast();

const onSumbit = () => {
  if(!text.value || !amount.value) {
    toast.error('Both fields are required');
    return;
  }
  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit('transactionSubmitted', transactionData);

  text.value = '';
  amount.value = '';
};
</script>