<template>
    <q-btn 
    v-if="show"
    @click="handleClick"
    text-color="black"
    padding="sm"
    icon="home"
    color="white"
    />
</template>

<script setup>
import { createBlock, defineComponent, ref, computed} from 'vue';

function handleClick(event) {
    dist.value = 0
}

const props = defineProps({
});

const dist = ref(500);
const show = computed(() => (dist.value > 100));

</script>