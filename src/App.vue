<template>
  <div class="app">
    <Header />
    <main class="container">
      <HomePage />
    </main>
    <Footer />
  </div>
</template>

<script>
import Header from './components/AppHeader.vue';
import Footer from './components/AppFooter.vue';
import HomePage from './components/HomePage.vue';

export default {
  components: { Header, Footer, HomePage },
};
</script>

<style>
.app {
  font-family: var(--body-font);
  color: var(--text-color);
  background-color: var(--background-color);
}
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}
</style>
