<template>
    <div>
        <div>
            <!-- 白框 -->
            <p v-if="random.motto" v-html="random.motto"></p>
        </div>
        <button @click="mottoAgain">我需要再一碗</button>
    </div>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted } from "vue";

const users = ref<{ motto: string }[]>([]); // 陣列，存 API 值
const random = reactive({ motto: "" }); // 只存隨機的 motto

//初始化時的動作  
onMounted(async () => {
    const response = await fetch("/json/motto.json");
    users.value = await response.json();
    
    mottoAgain();
});

function mottoAgain(){
    const randomIndex = Math.floor(Math.random() * users.value.length);
    return random.motto = users.value[randomIndex].motto;
}
</script>