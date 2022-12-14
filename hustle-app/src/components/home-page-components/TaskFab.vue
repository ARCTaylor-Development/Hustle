<template>
    <q-btn
    @click="handleClick"
    text-color="black"
    padding="sm"
    icon="add"
    color="white"/>
</template>

<script setup lang="ts">


    function handleClick(event) {
        console.log('Task button clicked');
    }

</script>