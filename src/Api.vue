<script setup>
import { ref, onMounted } from 'vue'

const post = ref([])

onMounted(async () => {
  const res = await fetch('https://jsonplaceholder.typicode.com/posts')
  post.value = await res.json()
})
</script>

<template>
  <v-container style="max-width: 600px;" class="py-6">
    <!-- ส่วนหัวข้อด้านบน -->
    <div class="d-flex align-center mb-6">
      <v-icon icon="mdi-post-outline" color="primary" size="large" class="mr-2"></v-icon>
      <h2 class="text-h5 font-weight-bold text-primary">List Posts</h2>
      <v-spacer></v-spacer>
      <v-chip size="small" color="primary" variant="tonal">
        {{ post.length }} โพสต์
      </v-chip>
    </div>

    <!-- รายการโพสต์แบบการ์ด -->
    <v-card
      v-for="list in post"
      :key="list.id"
      class="mb-4 rounded-lg"
      elevation="2"
      border
    >
      <v-card-item>
        <template v-slot:prepend>
          <v-chip color="primary" size="small" label class="font-weight-bold mr-2">
            #{{ list.id }}
          </v-chip>
        </template>
        <v-card-title class="text-subtitle-1 font-weight-bold text-wrap">
          {{ list.title }}
        </v-card-title>
      </v-card-item>

      <v-card-text class="text-body-2 text-medium-emphasis pt-1">
        {{ list.body }}
      </v-card-text>
    </v-card>
  </v-container>
</template>