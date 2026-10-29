<script setup>
import { ref } from 'vue'

const student = ref([
  { id: 1, name: 'นายสมปอง มองมา  ', score: 90 },
  { id: 1, name: 'นางรัญจวน ชวนฝัน ', score: 99 },
  { id: 1, name: 'นายหนุ่ม อุบอุ่น ', score: 80 },
  { id: 1, name: 'นางสมร เสมอ ', score: 89 },
])
</script>

<template>
  <h2>รายชื่อนักเรียน</h2>
  <ul>
    <li v-for="list in student">{{ list.name }} | ได้คะแนน {{ list.score }} คะแนน</li>
  </ul>
</template>
