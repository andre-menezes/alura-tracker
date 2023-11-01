<template>
  <header>
    <h1 class="is-flex is-flex-direction-column is-align-items-center is-justify-content-center">
      <img src="../assets/logo.png" alt="alura-tracker-logo">
      <button class="button is-info mt-6" @click="handleTheme">{{ btnDarkMode }}</button>
    </h1>
  </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'SideBar',
  emits: ['darkMode'],
  data() {
    return {
      darkMode: false
    }
  },
  computed: {
    btnDarkMode() {
      return this.darkMode ? 'Desativar Modo Escuro' : 'Ativar Modo Escuro';
    }
  },
  methods: {
    handleTheme() {
      this.darkMode = !this.darkMode;
      this.$emit('darkMode', this.darkMode);
    }
  }
});
</script>

<style>
header {
  background: var(--bg-secondary);
  height: 110vh;
  padding: 1rem;
  width: 100%;
}

@media only screen and (max-width: 768px) {
  header {
    height: auto;
    padding: 2.5rem;
  }
}
</style>