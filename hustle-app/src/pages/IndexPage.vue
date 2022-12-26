<template>

  <q-page v-touch-pan.mouse="handlePan">

  <task-bubble v-for="bubble in taskBubbles"
    :title="bubble.title"
    :color="bubble.title"
    :size="bubble.size"
    :position="bubble.position" />

  <q-page-sticky position="bottom-right" :offset="[18, 18]">
    <task-fab/>
  </q-page-sticky>

  <q-page-sticky position="bottom-left" :offset="[18,18]">
    <recenter-fab :show="true"/>
  </q-page-sticky>

  </q-page>

</template>

<script setup lang="ts">

  import { date } from 'quasar';
  import TaskBubble from 'src/components/home-page-components/TaskBubble.vue';
  import TaskFab from 'src/components/home-page-components/TaskFab.vue';
  import RecenterFab from 'src/components/home-page-components/RecenterFab.vue'
  import { createBlock, defineComponent, ref, computed, Ref} from 'vue';

  function handlePan(event) {
    let offX = event.delta.x;
    let offY = event.delta.y;

    Object.keys(posArrays.value).map(key => {
      let arr = posArrays.value[key as keyof object];
      posArrays.value[key as keyof object] = [arr[0]+offX, arr[1]+offY];
    });
  }

  function handleTaskClick(event) {
    taskFormOpen.value = true;
  }

  //Remove 'rem' and convert to int
  function sizeToInt(str: string) {
    return parseInt(str.substring(0, str.length-2))
  }

  const w = window.innerWidth;
  const h = window.innerHeight
  const r = sizeToInt('48px') * 1.5;

  const posArrays = ref({
    btn1: [w/2 - r, h/2 - r],
    btn2: [w/2 - r - 150, h/2 - r - 100],
    btn3: [w/2 - r + 150, h/2 - r + 50]
  });

  const taskBubbles = [
    {title: 'Test Bubble1', color: 'green', size: '48px', position: posArrays.value.btn1, id: 1},
    {title: 'Test Bubble2', color: 'purple', size: '20px', position: posArrays.value.btn2, id: 2},
    {title: 'Test Bubble3', color: 'orange', size: '32px', position: posArrays.value.btn3, id: 3}
  ]
  const taskFormOpen = ref(false);

</script>

<style scoped>
  .q-page {
    /* background-color: black; */
    background-image: url('..\assets\space-background.svg');
  }
</style>
