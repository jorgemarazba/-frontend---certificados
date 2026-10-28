<script setup lang="ts">
// Linea 2: Importas el Navbar que acabas de crear
import Navbar from './components/Navbar.vue'
// Linea 3: AGREGA ESTA NUEVA
import WorkspaceBar from './components/workspacebar.vue'
import DocumentosPanel from './components/Documentospenel.vue'  
</script>

<template>
  <!-- Linea 7: Aqui llamas al componente -->
  <!-- Es como decirle a Vue: "pon aqui mi navbar" -->
  <Navbar />
  <!-- Linea 9: AGREGA ESTO JUSTO DEBAJO DEL NAVBAR -->
  <WorkspaceBar />
  <DocumentosPanel />

  <main style="padding: 20px;">
    
  </main>
</template>


  <!-- Linea 10: Aqui luego ira tu contenido de certificados -->
  <main style="padding: 20px;">
    
  </main>


<style>
/* Linea 18: Reseteo para que el navbar quede pegado arriba */
body {
  margin: 0;
  font-family: Arial, sans-serif;
}

/* Evita desbordamiento en movil */
html, body {
  overflow-x: hidden;
  background-color: #f9fafb;
}c
</style>
