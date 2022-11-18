<template>

  <q-btn round :size="size">
    <h1>{{ title }}</h1>
  </q-btn>
        
  </template>

  
  
  <script lang="ts">
  import {
    defineComponent,
    PropType,
    computed,
    ref,
    toRef,
    Ref,
  } from 'vue';

  export default defineComponent({
    name: 'TaskBubble',
    props: {
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
      }
    },

    setup (props) {
      //Remove 'rem' and convert to int
      function sizeToInt(str: string) {
        return parseInt(str.substring(0, str.length-3))
      }

      const size = toRef(props, 'size')

      const fontSize = computed(() => {
        return ('' + sizeToInt(size.value) / 4.0 + 'rem');
      });

      return {
        bubbleFontSize: fontSize
      }

    }

  });


  
  </script>
  
  <style scoped>
    .q-btn {
      -ms-user-select: none;
      user-select: none;

      background-color: v-bind(color);
    }

    h1 {
      color: white;
      font-size: v-bind(bubbleFontSize);
    }

  </style>
  