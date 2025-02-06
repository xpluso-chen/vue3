<template>
    <ul>
        <li v-for="p in list" :key="p.index">
            車款:{{ p.name }},售價:{{ p.price }}
        </li>
    </ul>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'

defineProps(['list'])

</script>