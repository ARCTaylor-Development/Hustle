<template>
    <div class="taskFab">
        <q-btn
        text-color="black"
        padding="sm"
        icon="add"
        color="white"/>
    </div>
</template>

<script>
export default ({
    setup() {
        return {
            OnClick(){
                console.log("Add new task")
            }
        }
    }
})
</script>