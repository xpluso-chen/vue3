<template>
    <p v-if="random">JSON檔案中隨機跳出縣市:{{ random.name }}</p>
</template>

<script setup lang="ts">

// API
import { ref, reactive, onMounted } from "vue";
const users = ref([]);//陣列，用來裝API的值
const random = reactive([{name: '' }]);//只裝random要的

onMounted(async () => {
    const response = await fetch("/json/position.json");
    users.value = await response.json();

    if (users.value.length > 0) {
        const randomIndex = Math.floor(Math.random() * users.value.length);
        // random.id = users.value[randomIndex].id;
        random.name = users.value[randomIndex].name;
    }
});
</script>