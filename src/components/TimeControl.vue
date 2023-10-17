<template>
  <div class="column">
    <div class="is-flex is-align-items-center is-justify-content-space-between">
      <section>
        <strong>{{ timer }}</strong>
      </section>
      <button class="button" :disabled="!task || isTimeInProgress" @click="startTimer">
        <span class="icon">
          <i class="fas fa-play"></i>
        </span>
        <span>Iniciar</span>
      </button>
      <button class="button" :disabled="!isTimeInProgress" @click="stopTimer">
        <span class="icon">
          <i class="fas fa-stop"></i>
        </span>
        <span>Finalizar</span>
      </button>
    </div>
    <AlertDialog />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TimeControl',
  emits: ["taskIsDone"],
  props: {
    task: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      seconds: 0,
      count: 0,
      isTimeInProgress: false
    };
  },
  computed: {
    timer(): string {
      return new Date(this.seconds * 1000).toISOString().slice(11, 19);
    }
  },
  methods: {
    startTimer() {
      this.isTimeInProgress = true;
      this.count = setInterval(() => {
        this.seconds += 1;
      }, 1000);
    },
    stopTimer() {
      this.isTimeInProgress = false;
      clearInterval(this.count);
      this.$emit('taskIsDone', this.seconds);
      this.seconds = 0;
    }
  },
})
</script>