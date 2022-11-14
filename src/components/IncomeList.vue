<template>
    <div class="income-list">
      <IncomeItem v-for="obj in state.sortedIncome" :key="obj.id" :income="obj" @remove-item="removeItem" />
    </div>
  </template>
  
  <script setup>
  import IncomeItem from './IncomeItem.vue';

  const emit = defineEmits(['remove-item'])

  const props = defineProps({
 
    state: {
   type: Object,
 
  }});

 const removeItem = (id) => {
    emit( 'remove-item', id );
 }
 
  
  </script>
  
  <style scoped>
    .income-list {
      margin-top: 30px;
      padding: 15px;
      /* // #FFCE00 */
    }
  </style>