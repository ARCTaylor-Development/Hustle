<template>
  <q-page class="row items-center justify-evenly">

    <task-bubble title="Test Bubble" color="green" size="4rem"></task-bubble>
  </q-page>
</template>

<script lang="ts">
import TaskBubble from 'src/components/TaskBubble.vue';
import { defineComponent} from 'vue';

export default defineComponent({
  name: 'IndexPage',
  components: {TaskBubble }
});
</script>

<style scoped>
  .q-page {
    /* background-color: black; */
    background-image: url('..\assets\space-background.svg');
  }
</style>
