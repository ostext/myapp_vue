<script setup>
import { ref } from 'vue'
import { useStorage } from '@vueuse/core'

const data_list = useStorage('data_list', [])
const title = ref('')
const amount = ref('')

function add(type) {
  if (title.value == '' || amount.value == '') return
  data_list.value.push({ title: title.value, amount: Number(amount.value), type: type })
  title.value = ''
  amount.value = ''
}

function remove(index) {
  data_list.value.splice(index, 1)
}

function getBalance() {
  let total = 0
  for(const item of data_list.value) {
    if(item.type == 'income'){
      total += item.amount
    }else{
      total -= item.amount
    }
  }
  return total
}
</script>

<template>
  <v-container style="max-width: 500px;" class="text-center">
    <h1>รายรับ-รายจ่าย</h1>
    <h2>คงเหลือ {{ getBalance() }} บาท</h2>

    <v-text-field v-model="title" label="รายการ" />
    <v-text-field v-model="amount" label="จำนวนเงิน" type="number" />
    <v-btn color="green" class="mr-2" @click="add('income')">+ รายรับ</v-btn>
    <v-btn color="red" @click="add('expense')">- รายจ่าย</v-btn>
    <br>
    <v-list>
      <v-list-item v-for="(item, index) in data_list" :key="index">
        <div class="d-flex align-center">
          <span>{{ item.title }}</span>
          <v-spacer />
          <span :class="item.type == 'income' ? 'text-green' : 'text-red'" class="mr-2">
            {{ item.type == 'income' ? '+' : '-' }}{{ item.amount }}
          </span>
          <v-btn size="small" color="red" @click="remove(index)">ลบ</v-btn>
        </div>
      </v-list-item>
    </v-list>
  </v-container>
</template>