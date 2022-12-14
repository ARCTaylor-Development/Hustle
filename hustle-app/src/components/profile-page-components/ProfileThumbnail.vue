<template>
  <q-item>
    <q-item-section side>
      <q-avatar :size="size" >
        <img src="..\..\assets\bergquist-profile.jpeg" />
      </q-avatar>
  </q-item-section>

  <q-item-section>
      <h3>{{title}}</h3>
    </q-item-section>
</q-item>
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
    image: {
      type: String,
      required: true
    },
    size: {
      type: String,
      required: true
    }
  });

 
  console.log(props.image);
</script>

<style scoped>
  .q-item {
    width: 750px;
    height: 100px;
    margin: 10px;
    padding: none;
    background-color: lightgray;
  }

  .q-item-section {
    padding: none;
  }
</style>
