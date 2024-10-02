<script setup>
import MainHeader from './components/Header/MainHeader.vue'
import MainContent from './components/Main/MainContent.vue'
import MainFooter from './components/Footer/MainFooter.vue'
</script>

<template>
  <div class="layout-container">
    <div class="sidebar">
      <header>
        <MainHeader />
      </header>
      <footer>
        <MainFooter />
      </footer>
    </div>

    <main class="main-content">
      <MainContent />
    </main>
  </div>

</template>

<style scoped lang="scss">
.layout-container {
  display: flex;
  min-height: 100vh; // Almeno l'altezza della viewport

}

.sidebar {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 25%; // Definisce la larghezza per header e footer
  background-color: #f0f0f0; // Colore di sfondo per differenziare

}

.main-content {
  width: 75%; // Definisce la larghezza per il main content
  background-color: #ffffff; // Colore di sfondo per il main
}
</style>
