<template>
  <article class="message is-primary has-text-weight-medium">
    <div v-if="title" class="message-header">{{ title }}</div>
    <div class="message-body">
      {{ text }}
    </div>
  </article>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'MessageModal',
  props: {
    text: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: false
    }
  }
})
</script>
