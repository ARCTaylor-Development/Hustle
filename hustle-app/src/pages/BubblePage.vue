<template>

  <q-page v-touch-pan.mouse="handlePan">

  <task-bubble v-for="bubble in taskBubbles"
    :key = "bubble.id"
    :title="bubble.title"
    :color="bubble.color"
    :size="bubble.size"
    :position="bubble.position" />

  <q-page-sticky position="bottom-right" :offset="[18, 18]">
    <task-fab @click="handleTaskClick" :show="taskFormOpen"/>
  </q-page-sticky>

  <q-page-sticky position="bottom-left" :offset="[18,18]">
    <recenter-fab :show="true" @resetPos="handleResetPos" />
  </q-page-sticky>

  <q-page-sticky position="right" :offset="[10, 0]">
    <q-btn @click="$router.push('/profile')" color="white" text-color="black" icon="arrow_forward_ios"/>
  </q-page-sticky>

  </q-page>

</template>

<script setup lang="ts">

  import { date } from 'quasar';
  import TaskBubble from 'src/components/bubble-page-components/TaskBubble.vue';
  import TaskFab from 'src/components/bubble-page-components/TaskFab.vue';
  import RecenterFab from 'src/components/bubble-page-components/RecenterFab.vue'
  import { createBlock, defineComponent, ref, computed, Ref} from 'vue';
import { watch } from 'fs';

  function handlePan(event: any) {
    let offX = event.delta.x;
    let offY = event.delta.y;

    Object.keys(posArrays.value).map(key => {
      let arr = posArrays.value[key as keyof object];
      if(!arr) return;
      posArrays.value[key as keyof object] = [arr[0]+offX, arr[1]+offY];
    });
  }

  function handleResetPos(event: MouseEvent) {
    console.log("resetting position")
    Object.keys(posArrays.value).map(key => {
      let arr = originArrays.value[key as keyof object];
      if(!arr) return;
      posArrays.value[key as keyof object] = arr;
    });
  }

  function handleTaskClick(event: MouseEvent) {
    taskFormOpen.value = true;
  }

  function closeForm(event: MouseEvent) {
    taskFormOpen.value = false;
  }

  //Remove 'rem' and convert to int
  function sizeToInt(str: string) {
    return parseInt(str.substring(0, str.length-2))
  }

  const w = window.innerWidth;
  const h = window.innerHeight
  const r = sizeToInt('48px') * 1.5;

  const originArrays = ref({
    btn1: [w/2 - r, h/2 - r],
    btn2: [w/2 - r - 150, h/2 - r - 100],
    btn3: [w/2 - r + 150, h/2 - r + 50],
    btn4: [w/2 - r + 600, h/2 - r - 600],
    btn5: [w/2 - r - 150 + 600, h/2 - r - 100 - 600],
    btn6: [w/2 - r + 150 + 700, h/2 - r + 50 - 600]
  });

  const posArrays = ref({
    btn1: [w/2 - r, h/2 - r],
    btn2: [w/2 - r - 150, h/2 - r - 100],
    btn3: [w/2 - r + 150, h/2 - r + 50],
    btn4: [w/2 - r + 600, h/2 - r - 600],
    btn5: [w/2 - r - 150 + 600, h/2 - r - 100 - 600],
    btn6: [w/2 - r + 150 + 700, h/2 - r + 50 - 600]
  });

  const taskBubbles = computed( () => [
    {title: 'Test Bubble1', color: 'green', size: '48px', position: posArrays.value.btn1, id: 1},
    {title: 'Test Bubble2', color: 'purple', size: '20px', position: posArrays.value.btn2, id: 2},
    {title: 'Test Bubble3', color: 'orange', size: '32px', position: posArrays.value.btn3, id: 3},
    {title: 'Test Bubble4', color: 'red', size: '56px', position: posArrays.value.btn4, id: 4},
    {title: 'Test Bubble5', color: 'blue', size: '26px', position: posArrays.value.btn5, id: 5},
    {title: 'Test Bubble6', color: 'yellow', size: '42px', position: posArrays.value.btn6, id: 6}
  ])

  const taskFormOpen = ref(false);

</script>

<style scoped>
  .q-page {
    /* background-color: black; */
    background-image: url('..\assets\space-background.svg');
  }
</style>
