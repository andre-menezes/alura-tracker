<template>
  <header>
    <h1 class="is-flex is-align-items-center is-justify-content-center">
      <img src="../assets/logo.png" alt="alura-tracker-logo">
    </h1>
  </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'SideBar'
});
</script>

<style>
header {
  background: #0d3b66;
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