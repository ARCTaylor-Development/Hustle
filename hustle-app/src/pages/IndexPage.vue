<template>
  <q-page class="row items-center justify-evenly" style="background-color: darkblue;">
    <example-component
      title="Example component"
      active
      :todos="todos"
      :meta="meta"
    ></example-component>
  </q-page>
  <q-page-sticky position="bottom-right" :offset="[18, 18]">
  <task-fab></task-fab>
  </q-page-sticky>
</template>

<script lang="ts">
import { Todo, Meta } from 'components/models';
import TaskFab from 'src/components/TaskFab.vue';
import ExampleComponent from 'components/ExampleComponent.vue';
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'IndexPage',
  components: { ExampleComponent, TaskFab },
  setup () {
    const todos = ref<Todo[]>([
      {
        id: 1,
        content: 'ct1'
      },
      {
        id: 2,
        content: 'ct2'
      },
      {
        id: 3,
        content: 'ct3'
      },
      {
        id: 4,
        content: 'ct4'
      },
      {
        id: 5,
        content: 'ct5'
      }
    ]);
    const meta = ref<Meta>({
      totalCount: 1200
    });
    return { todos, meta };
  
  }
});
</script>