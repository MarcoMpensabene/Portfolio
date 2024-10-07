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

<style lang="scss">
.layout-container {
  display: flex;
  min-height: 100vh; // Almeno l'altezza della viewport

}

.sidebar {
  display: flex;
  flex-direction: column;
  width: 25%; // Definisce la larghezza per header e footer
  background-image: url("https://i.pinimg.com/1200x/84/da/14/84da14ed4cd64e9995650e9a7738cecc.jpg"); // Colore di sfondo per differenziare
  justify-content: space-between;

}

.main-content {
  width: 75%; // Definisce la larghezza per il main content
  background-color: #ffffff; // Colore di sfondo per il main
}
</style>
