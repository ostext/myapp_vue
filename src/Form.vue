<script setup>
 import {effect, ref} from 'vue'

 const input_OT = ref ('?')
 const input_value = ref('?')
 const money = ref(0)
 const total = ref('?')
 const tax = ref(0)
 
 function cal_total(){
  
  tax.value = (3/100)*input_value.value 
  money.value = input_value.value - tax.value
  total.value = input_OT.value + money.value

 }
 function clear_value(){
  input_OT.value = ref ('?')
  input_value.value = ref('?')
  total.value = ref('?')
  tax.value = ref('?')
  }
</script>P


<template>
  <h2>การใช้ Form</h2>
  <input type="number" placeholder="กรอกข้อมูลเงินเดือน" v-model="input_value">
  <input type="number" placeholder="กรอกข้อมูล OT " v-model="input_OT">
  <button @click="cal_total">คำนวณ</button>
  <button @click="clear_value">เคลียค่า</button>
  
  <p>คุณกรอกข้อมูล : {{ input_value }}</p>
  <p>OT : {{ input_OT }}</p>
  <P>หัก ณ ที่จ่าย (3%) :{{ tax }} </P>
  <p>รวม : {{ total }}</p>
</template>
