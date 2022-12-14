<template>
    <q-btn
    @click="handleClick"
    text-color="black"
    padding="sm"
    icon="add"
    color="white">
        <q-menu anchor="top right" self="bottom left">
            <h4>New Task</h4>
            <h6>Priority</h6>
            <q-rating
                v-model="ratingModel"
                size="2em"
                icon="warning"
                color="grey"
                :color-selected="ratingColors"/>
            <h1></h1>
        </q-menu>
    </q-btn>
<!-- icon="img:\src\assets\ExMark.svg" -->
</template>

<script>
import { ref } from 'vue'

export default {
  setup () {
    return {
      ratingModel: ref(4),
      ratingColors: [ 'light-green-13', 'yellow-12', 'amber-6', 'orange-10', 'red' ]
    }
  }
}
</script>