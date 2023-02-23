<template>
    <div class="task">
        <h3>{{ task.title }}</h3>
        <div class="icons">
            <i 
                class="bi bi-suit-heart-fill"
                :class="{active: task.isFav}"
                @click="taskStore.toggleFav(task.id)"
            ></i>
            <i 
                class="bi bi-trash3"
                @click="taskStore.deleteTask(task.id)"
            ></i>
        </div>
        
    </div>
</template>

<script>
import { useTaskStore } from '../stores/TaskStore'
export default {
    setup() {
        const taskStore = useTaskStore()
        
        return { taskStore }
    },
    props:['task'],
}
</script>

<style>

</style>