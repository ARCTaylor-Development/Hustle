<template>
    <q-btn 
    v-if=show
    @click="$router.push('/profile')"
    text-color="black"
    padding="sm"
    icon="home"
    color="white"
    />
</template>

<script setup>

function handleClick(event) {
    dist.value = 0
}

const props = defineProps({
    show: Boolean
});

</script>