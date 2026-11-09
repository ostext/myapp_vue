<script setup>
import {ref} from 'vue'

const user = ref('')
const pass = ref('')
const result = ref('')

function check_data(){
  if(user.value == 'ostext' && pass.value == '1559900579236ostext012353'){
    result.value = 'เข้าสู่ระบบสำเร็จ'
  }else{
    result.value = 'เข้าสู่ระบบไม่สำเร็จ'
  }
}
function clear_data(){
  user.value = ''
  pass.value = ''
  result.value = ''
}
</script>

<template>
  <v-container style="max-width: 400px;">
    <h1>日本</h1>

    <v-text-field v-model="user" label="Username" prepend-icon="mdi-account"></v-text-field>
    <v-text-field v-model="pass" label="Password" type="password" prepend-icon="mdi-lock"></v-text-field>

    <div class="text-center">
      <v-btn color="#CC66CC	" prepend-icon="mdi-login" class="mr-4" @click="check_data">
        เข้าสู่ระบบ
      </v-btn>
      <v-btn color="red" prepend-icon="mdi-cancel" @click="clear_data">
        ยกเลิก
      </v-btn>
      <p>{{ result }}</p>
    </div>
  </v-container>
</template>