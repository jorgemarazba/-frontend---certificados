<script setup lang="ts">
// Linea 2: Importas el Navbar que acabas de crear
import Navbar from './components/Navbar.vue'
</script>

<template>
  <!-- Linea 7: Aqui llamas al componente -->
  <!-- Es como decirle a Vue: "pon aqui mi navbar" -->
  <Navbar />

  <!-- Linea 10: Aqui luego ira tu contenido de certificados -->
  <main style="padding: 20px;">
    <h2>Contenido aqui...</h2>
  </main>
</template>

<style>
/* Linea 18: Reseteo para que el navbar quede pegado arriba */
body {
  margin: 0;
  font-family: Arial, sans-serif;
}
</style>
