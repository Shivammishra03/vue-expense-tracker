<script lang="ts" setup>
import { defineProps } from 'vue';

const props = defineProps({
    total: {
        type: Number,
        requried: true
    }
});

</script>

<template>
    <h4>Your Balance</h4>
    <h1 id="balance">${{props.total}}</h1>
</template>
