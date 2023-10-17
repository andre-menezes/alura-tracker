<template>
  <div class="column is-8" role="form" aria-label="Task form create">
    <input v-model="newTask" type="text" name="task" id="task" placeholder="Start a new task" class="input">
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: "TaskForm",
  emits: ['taskDescription'],
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
  }
})
</script>