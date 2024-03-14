<script  setup>
import Header from './components/header.vue';
import Balance from './components/balance.vue';
import IncomeExpense from './components/incomeExpense.vue';
</script>

<template>
  <Header/>
  <div class="container">
    <Balance />
    <IncomeExpense />
  </div>
</template>
