<template>
    <hr>
    <h2>車款:{{ car.name }}</h2>
    <h2>售價:{{ car.price }}</h2>
    <button @click=plusPrice>增加售價</button>
    <hr>
</template>

<script setup lang="ts">
import { reactive } from 'vue'
let car = reactive({ name: 'BMW', price: 99 })

function plusPrice() {
    car.price += 100;
}

</script>