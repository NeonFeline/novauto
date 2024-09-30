<script setup>
import Navigation from "./components/Navigation.vue";
import Footer from "./components/Footer.vue";
import Aside from "./components/Aside.vue";
import Cars from "./components/Cars.vue";
</script>

<template>
  <div class="content">
    <Navigation />

    <main class="main">
      <Aside />
      <Cars />
    </main>

    <Footer />
  </div>
</template>

<style lang="scss">
.content {
  width: 100vw;
  display: flex;
  flex-direction: column;
  font-family: sans-serif;
}

.main {
  display: flex;
  height: 100%;
  color: var(--color-dark-1);
  box-shadow: 0 1rem 1rem rgba(0, 0, 0, 0.05);
  z-index: 1;
}
</style>
