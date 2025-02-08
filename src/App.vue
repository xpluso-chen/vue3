<template>
  
    <Test class="logo">
</Test>

<div >
    <Test2 />
</div>
<div>
    <Test3 />
</div>

</template>

<script setup lang="ts">
import Test from './components/Test0207-api.vue'
import Test2 from './components/Test0208-motto.vue'
import Test3 from './components/Test0208-joke.vue'


</script>

<style lang="scss" scoped>
@use "sass:map";
.logo {
    border-radius: 50%;
    background-color: map.get($color, deepYellow );
    width: 300px;
    height: 300px;
}
.logo2{
    width: 600px;
    height: 600px;
    @extend %flex-center;
}
</style>
