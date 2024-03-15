<script  setup>
  import Header from './components/header.vue';
  import Balance from './components/balance.vue';
  import IncomeExpense from './components/incomeExpense.vue';
  import TransactionList from './components/transactionList.vue';
  import AddTransaction from './components/addTransaction.vue';
  import { ref, computed, onMounted } from 'vue';
  import { useToast } from "vue-toastification";

  const toast = useToast();

  const transactions = ref([]);
  const saveTransactionToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value));
  }
  onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));
    if (savedTransactions) {
      transactions.value = savedTransactions;
    }
  });

  const total = computed(() =>{
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
  });

  const income = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
  });
  const expenses = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
  });
  const generateUniqueId = () => {
    return Math.floor(Math.random() * 1000000);
  };
  const handleTransactionSubmitted = (transactionData) => {
    transactions.value.push({
      id:generateUniqueId(),
      ...transactionData
    });
    saveTransactionToLocalStorage();
    toast.success("Added a new transaction");
  };

  const handleTransactionDeleted = (id) =>{
    const filteredTransactions = transactions.value.filter((transaction)=> transaction.id !== id );
    transactions.value= filteredTransactions;
    saveTransactionToLocalStorage();
    toast.success('Removed the transaction');
  };

</script>

<template>
    <Header></Header>
  <div class="container">
    <Balance :total="total"/>
    <IncomeExpense :income="income" :expenses="expenses" />
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
  </div>
</template>
