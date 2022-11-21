<template>
  <q-page-sticky position="top-left" :offset="position">
    <q-btn round :size="size">
      <h1>{{ title }}</h1>
    </q-btn>
  </q-page-sticky>
        
  </template>

  
  
  <script setup lang="ts">
    import {
      defineComponent,
      PropType,
      computed,
      ref,
      toRef,
      Ref
    } from 'vue';

    // name: 'TaskBubble'
    
    const props = defineProps({
      title: {
        type: String,
        required: true
      },
      size: {
        type: String,
        required: true
      },
      color: {
        type: String,
        required: true
      },
      position: {
        type: Array as PropType<number[]>,
        required: true
      }
    });

    //Remove 'rem' and convert to int
    function sizeToInt(str: string) {
      return parseInt(str.substring(0, str.length-2))
    }

    const fontSize = computed(() => {
      return ('' + sizeToInt(props.size) / 4.0 + 'px');
    });

  </script>
  
  <style scoped>

    .q-page-sticky {
      -ms-user-select: none;
      user-select: none;
    }
    .q-btn {
      background-color: v-bind(color);
    }

    h1 {
      color: white;
      font-size: v-bind(fontSize);
    }

  </style>
  