<template>
    <hr>
    <h2>車款:{{ car.name }}</h2>
    <h2>售價:{{ car.price }}</h2>
    <h3>{{ sumString }}</h3>
    <hr>
</template>

<script setup lang="ts">

import { computed, reactive } from 'vue'
let car = reactive({ name: 'BMW', price: 99 })
let sumString = computed(() => {
    return car.name + car.price
})

</script>