<script setup>
import { ref } from 'vue'

const Task = ref('')
const Task_List = ref([])
const alert_status = ref(false)

function add_task() {
    alert_status.value = false
    if (Task.value != "") {
        Task_List.value.push(Task.value)
        Task.value = ""
    }
    else {
        alert_status.value = true
    }
}

function del_task(index) {
    Task_List.value.splice(index, 1)
}
</script>

<template>
    <v-container style="max-width: 500px;" class="text-center">
        <h1>To Do List</h1>
        <v-alert v-if="alert_status"
        text="กรุณาระบุสิ่งที่อยากจะทำ"
        type="warning">
        </v-alert>
        <br>
        <v-text-field
            v-model="Task"
            label="บอกสิ่งที่คุณอยากจะทำ"
            prepend-icon="mdi-playlist-edit">
        </v-text-field>

        <v-btn
            color="green"
            prepend-icon="mdi-plus"
            @click="add_task">
            เพิ่มรายการ
        </v-btn>

        <ol class="text-left">
            <li v-for="(list, index) in Task_List">
                <h3>{{ list }}</h3> <v-btn color="red" size="small" prepend-icon="mdi-delete" @click="del_task(index)">ลบ</v-btn>
                <v-divider></v-divider>
            </li>
        </ol>
    </v-container>
</template>
เขียนข้อความ
เขียนถึง 2/1
