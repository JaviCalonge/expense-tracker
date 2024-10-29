<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <IncomeExpsense :income="+income" :expense="+expense"/>
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpsense from "./components/IncomeExpsense.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { ref, computed, onMounted } from "vue";
import {useToast} from 'vue-toastification'

const toast = useToast()

const transactions = ref([])

onMounted(() => {
  const savedTransitions = JSON.parse(localStorage.getItem("transactions"))

  if(savedTransitions) {
    transactions.value = savedTransitions
  }
})

const total = computed (() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0).toFixed(2)
})

const income = computed (() => {
  return transactions.value
  .filter((transactions) => transactions.amount > 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0).toFixed(2)
})

const expense = computed (() => {
  return transactions.value
  .filter((transactions) => transactions.amount < 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0).toFixed(2)
})

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: randomId(),
    text: transactionData.text,
    amount: transactionData.amount
  })
  saveTransitionsToLocalStorage()
  toast.success("Transaction added")
}

const randomId = () => {
  return Math.floor(Math.random() * 10000)
}

const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id)
  saveTransitionsToLocalStorage()
  toast.success("Transaction deleted")
}

const saveTransitionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value))
}

</script>