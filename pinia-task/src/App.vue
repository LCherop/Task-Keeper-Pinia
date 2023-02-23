<template>
  <main>
    <header>
      <img src="./assets/icons/checkmark.svg" alt="checkmark logo">
      <h1>Task Keeper</h1>
    </header>

    <!-- Add New Task -->
    <div class="new-task-form">
      <AddTask />
    </div>

    <!-- filter -->
    <div class="filter">
      <button class="btn" @click="filter = 'all'">All Tasks</button>
      <button class="btn" @click="filter = 'faves'"> Fav Tasks</button>
    </div>

    <!-- Loading -->
    <div class="loading" v-if="loading">
      Loading tasks...
    </div>

    <!-- Task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ totalCount }} tasks left to do</p>
      <div v-for="task in tasks" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>

    <!-- Favorite task list -->
    <div class="task-list" v-if="filter === 'faves'">
      <p>You have {{ favCount }} faves left to do</p>
      <div v-for="task in faves" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>

    <button @click="$reset">reset state</button>
  </main>
</template>

<script>
import { ref } from 'vue';
import { useTaskStore } from './stores/TaskStore';

// Components
import AddTask from './components/AddTask.vue';
import TaskDetails from './components/TaskDetails.vue';
import { storeToRefs } from 'pinia';



export default {
  setup(){
    const taskStore = useTaskStore()

    //Use StoreToRefs to avoid something like taskStore.loading
    //Works for everything except actions
    const { tasks,loading,faves,totalCount,favCount } = storeToRefs(taskStore)

    //fetch tasks
    taskStore.getTasks()
    
    const filter = ref('all')

    return { taskStore, filter,tasks,loading,faves,totalCount,favCount}
  },
  components:{
    TaskDetails,
    AddTask,
  }
}
</script>

<style>
@import url('bootstrap-icons');

/* @import 'bootstrap-icons'; */

</style>