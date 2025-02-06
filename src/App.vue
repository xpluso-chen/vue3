<template>
  <Test4 :list="car1"/>
</template>

<script setup lang="ts">
import Test4 from './components/Test0206-props.vue'
import { reactive } from 'vue'

let car1 = reactive([
{ name: 'BMW1', price: 99 },
{ name: 'BMW2', price: 99 },
{ name: 'BMW3',price: 99 },
{ name: 'BMW4', price: 99 }
])
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
