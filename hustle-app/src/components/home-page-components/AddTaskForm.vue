<template>
  <q-form anchor="top right" self="bottom left" transition-show="fade">
    <h4>New Task</h4>
    <h6>Priority</h6>
    <q-input
        filled
        v-model="name"
        label="Task name *"
        hint="Label for your task"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please input a task name']"
    />

    <q-input
        filled
        type="number"
        v-model="age"
        label="Task description"
        hint="Short description of task"
        lazy-rules
    />
    <q-rating
        v-model="ratingModel"
        size="2em"
        icon="warning"
        color="grey"
        :color-selected="ratingColors"/>
  </q-form>

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

    const props = defineProps({
     
    });

  </script>
  
  <style scoped>
  .q-form {
          background-color: white;
          width: 100vw;
          height: 100vh;
      }
  </style>
  