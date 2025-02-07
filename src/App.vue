<template>
  
    <Test class="logo">
</Test>

13
<Test2 class="logo"/>
</template>

<script setup lang="ts">
import Test from './components/Test0207-api.vue'
import Test2 from './components/Test0203-ref.vue'


</script>

<style lang="scss" scoped>
@use "sass:map";
.logo {
    border-radius: 50%;
    background-color: rgb(211, 145, 57);
    width: 300px;
    height: 300px;
    color: map.get($color, nav-deepblue );
}
</style>
