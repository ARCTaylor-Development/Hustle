<template>

  <q-page v-touch-pan.mouse="handlePan" class="">

    <task-bubble title="Test Bubble" color="green" size="48px" :position=posArrays.btn1></task-bubble>
    <task-bubble title="Test Bubble" color="purple" size="20px" :position=posArrays.btn2></task-bubble>
    <task-bubble title="Test Bubble" color="orange" size="32px" :position=posArrays.btn3></task-bubble>

  <q-page-sticky position="bottom-right" :offset="[18, 18]">
  <task-fab></task-fab>
  </q-page-sticky>
  </q-page>
</template>

<script setup lang="ts">

  import { date } from 'quasar';
  import TaskBubble from 'src/components/TaskBubble.vue';
  import TaskFab from 'src/components/TaskFab.vue';
  import { createBlock, defineComponent, ref, computed, Ref} from 'vue';

  function handlePan(event) {
    let offX = event.delta.x;
    let offY = event.delta.y;

    Object.keys(posArrays.value).map(key => {
      let arr = posArrays.value[key as keyof object];
      posArrays.value[key as keyof object] = [arr[0]+offX, arr[1]+offY];
    });
  }

  //Remove 'rem' and convert to int
  function sizeToInt(str: string) {
    return parseInt(str.substring(0, str.length-2))
  }

  const w = window.innerWidth;
  const h = window.innerHeight
  const r = sizeToInt("48px") * 1.5;

  const posArrays = ref({
    btn1: [w/2 - r, h/2 - r],
    btn2: [w/2 - r - 150, h/2 - r - 100],
    btn3: [w/2 - r + 150, h/2 - r + 50]
  });

</script>

<style scoped>
  .q-page {
    /* background-color: black; */
    background-image: url('..\assets\space-background.svg');
  }
</style>
