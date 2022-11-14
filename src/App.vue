

<template>
 <Header :totalIncome="state.totalIncome" />
 <Form :state="state" @add-income="AddIncome" />
 <IncomeList :state="state" @remove-item="removeItem" />
</template>

<script setup>

import Header from './components/Header.vue';
import Form from './components/Form.vue';
import IncomeList from './components/IncomeList.vue';

import { reactive,computed } from 'vue'; 

const state = reactive({
  income:[],
  sortedIncome: computed(() => {
      let temp = [];
      
      temp = state.income.sort(function (a, b) {
        return b.date - a.date;
      });
      return temp;
   }),
  totalIncome: computed(()=>{
   
    let temp =0;
    if(state.income.length >0){

      for(let i=0;i<state.income.length;i++){
        temp += state.income[i].value;
      }
    }

    return temp;

  })
});

const AddIncome = (data) => {

  let d = data.date.split("-");
      let newD = new Date(d[0], d[1], d[2]);
      state.income = [...state.income, {
        id: Date.now(),
        desc: data.desc,
        value: parseInt(data.value),
        date: newD.getTime()
      }]
}
const removeItem = (id) => {

  state.income = state.income.filter(v => v.id != id);
}

</script>

<style scoped>
 
</style>
