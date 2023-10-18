
import TimeControl from './TimeControl.vue';
<template>
  <div class="box has-text-weight-bold my-2">
    <div class="columns">
      <div class="column is-7">{{ task || 'Tarefa sem descrição' }}</div>
      <div class="column">{{ time }}</div>
      <ActionButton styleContent="button is-dark pr-1" icon="fas fa-trash" @action="removeItem" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ActionButton from './ActionButton.vue';
import { TaskList } from '@/utils/types';

export default defineComponent({
  name: 'TaskItem',
  emits: ['action'],
  components: { ActionButton },
  props: {
    task: {
      type: String,
      required: true
    },
    time: {
      type: String,
      required: true
    }
  },
  methods: {
    removeItem() {
      const value: TaskList = { task: this.task, time: this.time }
      this.$emit('action', value);
    }
  }
})
</script>
