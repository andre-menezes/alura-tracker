<template>
  <div class="column">
    <div class="is-flex is-align-items-center is-justify-content-space-between">
      <section>
        <strong>{{ timer }}</strong>
      </section>
      <ActionButton styleContent="button is-success" label="INICIAR" icon="fas fa-play"
        :disabled="!task || isTimeInProgress" @action="startTimer" />
      <ActionButton styleContent="button is-danger" label="FINALIZAR" icon="fas fa-stop" :disabled="!isTimeInProgress"
        @action="stopTimer" />
    </div>
    <AlertDialog />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import ActionButton from './ActionButton.vue';

export default defineComponent({
  name: 'TimeControl',
  emits: ["taskIsDone"],
  components: { ActionButton },
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
    startTimer(): void {
      this.isTimeInProgress = true;
      this.count = setInterval(() => {
        this.seconds += 1;
      }, 1000);
    },
    stopTimer(): void {
      this.isTimeInProgress = false;
      clearInterval(this.count);
      this.$emit('taskIsDone', this.seconds);
      this.seconds = 0;
      const audio = new Audio(process.env.BASE_URL + 'endTask.mp3');
      audio.play();
    }
  },
})
</script>