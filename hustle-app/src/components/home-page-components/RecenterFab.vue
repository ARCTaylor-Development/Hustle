<template>
    <q-btn 
    v-if="show"
    @click="$router.push('/profile')"
    text-color="black"
    padding="sm"
    icon="home"
    color="white"
    />
</template>

<script setup lang="ts">
import { createBlock, defineComponent, ref, computed} from 'vue';

function handleClick(event) {
    dist.value = 0
}

const dist = ref(500);
const show = computed(() => (dist.value > 100));

</script>