<template>    
    <q-btn
    @click="show = true;"
    text-color="black"
    padding="sm"
    icon="add"
    color="white" >
    </q-btn>

    <q-menu v-if="show" square cover persistent max-width="100vw" max-height="100vh">
            <q-form anchor="top right" self="bottom left" transition-show="fade">
                <div>
                    <q-btn @click="show = false;" class="float-right" icon="close" color="red" text-color="white" />
                    <h1>New Task</h1>
                </div>
                <h2>Priority</h2>
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
                    v-model="description"
                    label="Task description"
                    hint="Short description of task"
                    lazy-rules
                />
                <q-input
                    filled
                    type="date"
                    v-model="dueDate"
                    label="Due date"
                    hint="Date to complete task by"
                    lazy-rules
                />
                <q-rating
                    v-model="ratingModel"
                    size="2em"
                    icon="warning"
                    color="grey"
                    :color-selected="ratingColors"/>
                
            </q-form>
        </q-menu>

<!-- icon="img:\src\assets\ExMark.svg" -->
</template>

<script setup>
    import { ref } from 'vue'
    import AddTaskForm from 'src/components/bubble-page-components/RecenterFab.vue'

    const props = defineProps({
    });

    const show = ref(false);

    const ratingModel = ref(4);
    const ratingColors = [ 'light-green-13', 'yellow-12', 'amber-6', 'orange-10', 'red' ];

    const name = ref(null);
    const description = ref(null);
    const dueDate = ref(null);


</script>

<style scoped>
    .q-form {
        width: 100vw;
        height: 100vh;
    }

    .q-input {
        margin-bottom: 50px;
        padding: 10px;
    }

    h1, h2 {
        margin-top: 0px;
        text-align: center;
        display:block;
    }
    
    .q-rating {
        margin-left: 20px;
        margin-bottom: 50px;
    }

</style>