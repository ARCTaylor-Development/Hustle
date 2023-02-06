<template>
    <q-btn 
    v-if=show
    @click="$emit('resetPos')"
    text-color="black"
    padding="sm"
    icon="home"
    color="white"
    />
</template>

<script setup>
import { defineEmits,watch,ref } from 'vue'
    
const emit = defineEmits(['resetPos']);

function handleClick(event) {
    dist.value = 0
}

const props = defineProps({
    show: Boolean
});

</script>