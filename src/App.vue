<template>
  <main class="columns is-gapless is-multiline">
    <div class="column is-one-quarter">
      <SideBar />
    </div>
    <div class="column is-three-quarter">
      <div class="box">
        <div class="columns">
          <TaskForm :task="task" @taskDescription="updateTask" />
          <TimeControl :task="task" @taskIsDone="addTask" />
        </div>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import SideBar from './components/SideBar.vue';
import TaskForm from './components/TaskForm.vue';
import TimeControl from './components/TimeControl.vue';
import { TaskList } from './utils/types';

export default defineComponent({
  name: 'App',
  components: { SideBar, TaskForm, TimeControl },
  data() {
    return {
      task: '',
      taskList: [] as TaskList[]
    }
  },
  methods: {
    updateTask(value: string) {
      this.task = value;
    },
    addTask(timeInSeconds: number) {
      const time = new Date(timeInSeconds * 1000).toISOString().slice(11, 19);
      this.taskList.push({ task: this.task, time })
      this.task = ''
    }
  }
});
</script>

<style></style>
