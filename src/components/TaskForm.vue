<template>
  <div class="column is-7" role="form" aria-label="Task form create">
    <input v-model="newTask" type="text" placeholder="Qual tarefa deseja iniciar?" class="input" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: "TaskForm",
  emits: ['taskDescription', 'add'],
  props: {
    task: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      newTask: this.task
    }
  },
  watch: {
    task(value) {
      this.newTask = value
    },
    newTask(value) {
      this.$emit('taskDescription', value);
    }
  },
  methods: {
    addTask() {
      this.$emit('add')
    }
  }
})
</script>