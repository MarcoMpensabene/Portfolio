<script setup>
import MainHeader from './components/Header/MainHeader.vue'
import MainContent from './components/Main/MainContent.vue'
import MainFooter from './components/Footer/MainFooter.vue'
</script>

<template>
  <header>
    <MainHeader />
  </header>

  <main>
    <MainContent />
  </main>

  <footer>
    <MainFooter />
  </footer>
</template>

<style scoped lang="scss">
main,
footer,
header {
  max-width: 70vw;
  margin: 0 auto;
  margin-bottom: 3rem;
}
</style>
