<template>
  <div>
    <ul>
      <li v-for="(item, index) in list" :key="index">
        <TaskItem :task="item.task" :time="item.time" @action="removeItem" />
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { TaskList } from '@/utils/types';
import TaskItem from './TaskItem.vue';

export default defineComponent({
  name: 'ItemList',
  emits: ['action'],
  components: { TaskItem },
  props: {
    list: {
      type: Array as () => TaskList[],
    }
  },
  methods: {
    removeItem(value: TaskList): void {
      this.$emit('action', value)
    }
  }
})
</script>