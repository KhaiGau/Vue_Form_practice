<script setup>
import UserForm from './components/UserForm.vue';
</script>

<template>
  <div>
    <a href="https://vite.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <UserForm />
</template>

<style scoped>
#app {
  width: 100%;
  max-width: none;
  margin: 0;
  padding: 1rem;
}
.logo,.logo.vue {
  margin: 0;
  height: 10em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
  justify-content: center;
  align-items: center;
  
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
