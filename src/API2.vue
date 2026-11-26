<script setup>
import { ref, onMounted } from 'vue'

const title = ref('')
const className = ref('')
const teacher = ref('')
const date = ref('')
const students = ref([])
const detail = ref(null)

onMounted(async () => {
    try {
        const res = await fetch('https://ntc2.technicnan.ac.th/public/nan_api/')
        const data = await res.json()

        console.log(data)

        title.value = data.title
        className.value = data.class
        teacher.value = data.teacher
        date.value = data.date

        students.value = data.data
    } catch (e) {
        console.error('ดึงข้อมูลไม่สำเร็จ', e)
    }
})
</script>

<template>
    <v-container>

        <!-- หัวเว็บ -->
        <v-card class="pa-4 mb-5">
            <h2>{{ title }}</h2>
            <p>ชั้น : {{ className }}</p>
            <p>ครูที่ปรึกษา : {{ teacher }}</p>
            <p>วันที่ : {{ date }}</p>
        </v-card>

        <!-- รายชื่อนักเรียน -->
        <v-row>
            <v-col
                cols="12"
                sm="6"
                md="3"
                v-for="list in students"
                :key="list.student_id"
            >
                <v-card
                    class="pa-3 text-center"
                    @click="detail = list"
                >
                    <!-- คนที่ 10 ไม่มีรูป: เว้นที่ไว้ให้การ์ดสูงเท่ากัน -->
                    <v-img
                        v-if="list.no !== 10"
                        :src="list.image_url"
                        height="180"
                        cover
                    ></v-img>
                    <div v-else style="height: 180px"></div>

                    <p>เลขที่ {{ list.no }}</p>
                    <p>{{ list.full_name }}</p>
                    <p>รหัส {{ list.student_id }}</p>
                    <p>เพศ : ไม่มีข้อมูล</p>
                </v-card>
            </v-col>
        </v-row>

        <!-- หน้าต่างรายละเอียด -->
        <v-dialog
            :model-value="!!detail"
            @update:model-value="detail = null"
            max-width="400"
        >
            <v-card class="pa-4 text-center" v-if="detail">
                <h2>รายละเอียดนักเรียน</h2>

                <v-img
                    v-if="detail.no !== 10"
                    :src="detail.image_url"
                    height="250"
                ></v-img>

                <p>เลขที่ {{ detail.no }}</p>
                <p>{{ detail.full_name }}</p>
                <p>รหัส {{ detail.student_id }}</p>

                <v-btn color="primary" @click="detail = null">
                    ปิด
                </v-btn>
            </v-card>
        </v-dialog>

    </v-container>
</template>