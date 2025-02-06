<template>
    <p v-if="random">{{ random }}</p>
</template>

<script setup lang="ts">

// API
import { ref, onMounted } from "vue";
const users = ref([]);//陣列，用來裝API的值
const random = ref('');//只裝random要的

onMounted(async () => {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    users.value = await response.json();

    if (users.value.length > 0) {
        const randomIndex = Math.floor(Math.random() * users.value.length);
        random.value = users.value[randomIndex].id + users.value[randomIndex].name;
    }
});
</script>