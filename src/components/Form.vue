<template>
    <form @submit.prevent="FormHandler">
      <input type="text" placeholder="Income Description..." v-model="formData.desc" />
      <input type="number" placeholder="Income Value..." v-model="formData.amount" />
      <input type="date" placeholder="Income Date..." v-model="formData.date" />
      <input type="submit" value="SUBMIT"  />
    </form>
  </template>
  
  <script setup>
  import { reactive } from 'vue';

  const props = defineProps({
   
   state: {
     type: Object,
   
   },
   
 })

  const emit = defineEmits(['add-income'])

  const formData = reactive({
        desc: null,
        amount: null,
        date: null
      });


    const FormHandler = () => {

        if(formData.desc && formData.amount && formData.date){
            emit("add-income", {
                desc: formData.desc,
                value: formData.amount,
                date: formData.date
            });
            formData.desc = null;
            formData.amount = null;
            formData.date = null;
        }

    }

    


  </script>
  
  <style scoped>
    form {
      display: flex;
      justify-content: center;
      margin-top: 30px;
    }
    form input {
      color: #888;
      border: none;
      outline: none;
      font-size: 20px;
    }
    form input::placeholder {
      color: #AAA;
    }
    form input:not([type="submit"]) {
      display: block;
      background: #FFF;
      border: none;
      outline: none;
      padding: 5px 15px;
    }
    form input[type="submit"] {
      display: block;
      background: none;
      border: none;
      outline: none;
      color: #FFF;
      font-weight: 500;
      text-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
      padding: 5px 15px;
      background-color: rgb(128,0,128);
      cursor: pointer;
    }
    form input:first-of-type {
      border-radius: 8px 0px 0px 8px;
    }
    form input:last-of-type {
      border-radius: 0px 8px 8px 0px;
    }
  </style>