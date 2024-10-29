<script setup>

//LA MANERA MODERNA DE HACERLO: con setup en la etiqueta script

// const transactions = [
//   { id: 1, text: "Lidl", amount: -89},
//   { id: 2, text: "Factura Luz", amount: -49.98},
//   { id: 3, text: "Nómina", amount: 2400}
// ]

//UNA MANERA DE HACERLO
 //export default {
  // data() {
  //   return {
  //     transactions: [
  //       { id: 1, text: "Lidl", amount: -89},
  //       { id: 2, text: "Factura Luz", amount: -49.98},
  //       { id: 3, text: "Nómina", amount: 2400}
  //     ]
  //   }
  // }

//OTRA MANERA DE HACERLO
 //export default {
  // setup() {
  //   const transactions = [
  //     { id: 1, text: "Lidl", amount: -89},
  //     { id: 2, text: "Factura Luz", amount: -49.98},
  //     { id: 3, text: "Nómina", amount: 2400}
  //   ];
  //   return {
  //     transactions
  //   }
  // }

  import { defineProps } from 'vue';

  const props = defineProps({
    transactions: {
      type: Array,
      Required: true
    }
  })

  const emit = defineEmits (["transactionDeleted"])

  const deleteTransaction = (id) => {
    emit("transactionDeleted", id)
  }

</script>

<template>
  <h3>History</h3>
      <ul id="list" class="list">
        <li v-for="transaction in transactions" :key="transaction.id"
          :class="transaction.amount < 0 ? 'minus' : 'plus'">
          {{ transaction.text }} <span>{{ transaction.amount }} €</span><button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
        </li>
      </ul>
</template>