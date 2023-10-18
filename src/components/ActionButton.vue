<template>
  <button :class="styleContent" :disabled="disabled" @click="action">
    <span class="icon">
      <i :class="icon"></i>
    </span>
    <span>{{ label }}</span>
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
  name: 'ActionButton',
  emits: ["action"],
  props: {
    styleContent: {
      type: String,
      default: 'button is-primary',
    },
    disabled: {
      type: Boolean,
      default: false,
      required: false
    },
    icon: {
      type: String,
      default: '',
    },
    label: {
      type: String,
      required: false,
    },
  },
  methods: {
    action(): void {
      this.$emit('action');
    }
  }
})
</script>