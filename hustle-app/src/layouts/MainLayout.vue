<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'MainLayout',

  setup () {
    return {}
  }
});
</script>
