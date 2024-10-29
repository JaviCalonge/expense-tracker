<script setup>
   import { defineProps } from 'vue';

   const props = defineProps({
      total: {
         type: Number,
         Required: true
   }
})
</script>

<template>
   <div class="container">
      <h4>Your Balance</h4>
      <h1 id="balance">{{ total }} €</h1>
    </div>
</template>