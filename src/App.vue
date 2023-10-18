<template>
  <main class="columns is-gapless is-multiline is-fullheight">
    <div class="column is-one-quarter">
      <SideBar />
    </div>
    <div class="column is-three-quarter">
      <div class="box">
        <div class="columns">
          <TaskForm :task="task" @taskDescription="updateTask" @add="addTask" />
          <TimeControl :task="task" @taskIsDone="addTask" />
        </div>
        <div v-if="taskList.length">
          <div class="is-flex is-justify-content-space-between">
            <h1 class="title is-4 has-text-weight-bold">Histórico de Tarefas</h1>
            <ActionButton styleContent="button is-danger is-small" label="LIMPAR LISTA" icon="fas fa-ban"
              @action="clearTaskList" />
          </div>
          <ItemList :list="taskList" @action="removeTask" />
        </div>
      </div>
    </div>

    <div v-if="isTaskComplete" class="modal is-active">
      <div class="modal-content">
        <MessageModal text="Tarefa finalizada com sucesso!" />
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import SideBar from './components/SideBar.vue';
import TaskForm from './components/TaskForm.vue';
import TimeControl from './components/TimeControl.vue';
import ItemList from './components/ItemList.vue';
import { TaskList } from './utils/types';
import ActionButton from './components/ActionButton.vue';
import MessageModal from './components/MessageModal.vue';

export default defineComponent({
  name: 'App',
  components: { ItemList, SideBar, TaskForm, TimeControl, ActionButton, MessageModal },
  data() {
    return {
      task: '',
      taskList: [] as TaskList[],
      isTaskComplete: false
    }
  },
  created() {
    const tasks = localStorage.getItem('tasks');
    this.taskList = tasks ? JSON.parse(tasks) : [];
  },
  methods: {
    updateTask(value: string) {
      this.task = value;
    },
    addTask(timeInSeconds: number) {
      this.taskComplete();
      const time = new Date(timeInSeconds * 1000).toISOString().slice(11, 19);
      this.taskList.unshift({ task: this.task, time });
      this.task = '';
      localStorage.setItem('tasks', JSON.stringify(this.taskList));
    },
    removeTask(value: TaskList) {
      this.taskList = this.taskList.filter((item) => item.task !== value.task && item.time !== value.time);
      localStorage.setItem('tasks', JSON.stringify(this.taskList));
    },
    clearTaskList() {
      this.taskList = [];
      localStorage.setItem('tasks', JSON.stringify(this.taskList));
    },
    taskComplete() {
      this.isTaskComplete = true;
      setTimeout(() => {
        this.isTaskComplete = false;
      }, 4000);
    }
  }
});
</script>

<style>
.modal-content {
  top: 0.8rem;
  position: absolute;
  width: auto;
}
</style>
