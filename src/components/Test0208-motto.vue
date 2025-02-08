<template>
    <p v-if="random.motto" v-html="random.motto"></p>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted } from "vue";

const users = ref<{ motto: string }[]>([]); // 陣列，存 API 值
const random = reactive({ motto: "" }); // 只存隨機的 motto

onMounted(async () => {
    const response = await fetch("/json/motto.json");
    users.value = await response.json();

    if (users.value.length > 0) {
        const randomIndex = Math.floor(Math.random() * users.value.length);
        random.motto = users.value[randomIndex].motto;
    }
});
</script>