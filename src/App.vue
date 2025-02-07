<template>
  
    <Test class="logo">
</Test>

13
<div class="logo2">
    <ul>
        <li>123</li>
    </ul>
    <Test2 />
</div>

</template>

<script setup lang="ts">
import Test from './components/Test0207-api.vue'
import Test2 from './components/Test0203-ref.vue'


</script>

<style lang="scss" scoped>
@use "sass:map";
.logo {
    border-radius: 50%;
    background-color: map-get($color, bg-deepYellow );
    width: 300px;
    height: 300px;
    color: map.get($color, nav-deepblue );
}
.logo2{
    width: 600px;
    height: 600px;
    @extend %flex-center;
}
</style>
