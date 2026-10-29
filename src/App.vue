<script setup>
import {ref,reactive } from 'vue';

const loginStatus =ref(false)
const count =ref(0)
const detail = reactive({
  name :'บรรจง พากเพียร',
  cash : 99
})
function addCash(){
  detail.cash+=50
}
const student ={
  name :'ostext',
  department :'เทคโนโลยีสารสนเทศ',
  image : 'miku.png'
}
</script>

<template>
  <button @click="loginStatus =true">Login</button>
  <button @click="loginStatus =false">Logout</button>
  <p>{{ loginStatus }}</p>
  <P v-if="loginStatus==true">Login</P>
  <p v-else>Logout</p>

  <div v-if="loginStatus == true">
  <p>{{  detail.name }}มีเงิน{{ detail.cash }} บาท</p>
  <button @click="addCash">เพิ่มเงิน 50 บาท</button>
  
  <p>จำนวน : {{ count }}</p>
  <button @click="count+=123456789">เพิ่มจำนวน</button>
   <button @click="count-=123456789">ลดจำนวน</button>

  <h1>ข้อมูลนักเรียน</h1>
  <p>ชื่อ : {{ student.name }}</p>
  <p>สาขา : {{ student.department }}</p>
  <img :src="student.image">
</div>
</template>