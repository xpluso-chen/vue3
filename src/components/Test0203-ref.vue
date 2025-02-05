<template>
<hr>
<!-- 以下是0203的練習 -->
<h2>姓名:{{name}}</h2>
<h2>年齡:{{age}}</h2>
<button @click=plusAge>增加年紀</button>
</template>


<script setup lang="ts">
import {ref} from 'vue'
let name='奧米加咆嘯獸';
let age=ref(999);

function plusAge(){
age.value +=1;
}

</script>