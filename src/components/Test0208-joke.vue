<template>
    <div>
        <div>
            <!-- 白框 -->
            <p v-if="random.question" v-html="random.question"></p>
            <hr>
            <button @click="showAns">showAns</button>
            <!-- 顯示答案 -->
            <p v-if="random.ans" v-html="random.ans"></p>
        </div>
        <button @click="jokeAgain">不夠冷再一個</button>
    </div>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted } from "vue";

const users = ref<{ question: string,ans: string }[]>([]); // 陣列，存 API 值
const random = reactive({ question: "",ans:"" }); // 只存隨機的 motto
const randomIndex=ref<number | null>(null); // 用來記錄當前的索引

//初始化時的動作  
onMounted(async () => {
    const response = await fetch("/json/joke.json");
    users.value = await response.json();
    
    jokeAgain(); // 先顯示第一個問題
});

function jokeAgain(){
    randomIndex.value = Math.floor(Math.random() * users.value.length);
    random.question = users.value[randomIndex.value].question;
    random.ans = ""; // 清空答案，確保新的問題出來時，不會殘留舊的答案。
}
function showAns(){
    random.ans = users.value[randomIndex.value].ans;
}
</script>