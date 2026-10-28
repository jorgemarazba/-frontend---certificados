<template>
    <!-- NAVBAR-->
     <nav class="navbar">

        <!-- LADO IZQUIERDO:  logo y titulo-->
         <div class="left-section">

            <!--logo en assets-->
            <img src="@/assets/book.jpg" alt="logo" class="logo"/>

            <div class="titles">
                <!--titulo en negrita-->
                <h1 class="main-title">VAULT ARCHIMENT</h1>
        <!-- Linea 11: Subtitulo en cursiva -->
        <p class="subtitle">gestion documental</p>
      </div>
    </div>

    <!-- LADO DERECHO: Boton contador -->
    <div class="right-section">
      <!-- Linea 18: Este boton cuenta los documentos -->
      <button class="counter-btn">
        Documentos: {{ docCount }}
      </button>
    </div>
  </nav>
</template>

<script setup lang="ts">
// Linea 27: Aqui va la logica del contador
import { ref } from 'vue';

// ref = variable que Vue puede contar
// Inicia en 0
const docCount = ref(0);

// Funcion para cuando subas un documento luego la llamaras
// Ejemplo: docCount.value++
function incrementarDocumentos() {
  docCount.value++;
}

// Hacemos que la funcion este disponible
defineExpose({ incrementarDocumentos, docCount })
</script>

<style scoped>
/* Linea 45: Color azul oscuro universitario #0A2A5E */
.navbar {
  background-color: #0A2A5E;
  color: white;
  display: flex;
  justify-content: space-between; /* Izquierda y derecha separadas */
  align-items: center;
  padding: 12px 24px;
  height: 70px;
}
.left-section {
  display: flex;
  align-items: center;
  gap: 12px;
}
.logo {
  width: 45px;
  height: 45px;
  object-fit: contain;
  background: white;
  border-radius: 50%;
  padding: 3px;
}
.titles {
  display: flex;
  flex-direction: column;
}
.main-title {
  font-weight: 800; /* Negrita */
  font-size: 18px;
  letter-spacing: 1px;
  margin: 0;
  text-transform: uppercase;
}
.subtitle {
  font-style: italic; /* Cursiva */
  font-size: 13px;
  margin: 0;
  opacity: 0.9;
}
.right-section {
}
.counter-btn {
  background-color: white;
  color: #0A2A5E;
  border: none;
  padding: 8px 16px;
  border-radius: 20px;
  font-weight: bold;
  cursor: pointer;
}

/* RESPONSIVE NAVBAR */
@media (max-width: 768px) {
  .navbar {
    height: auto;
    padding: 10px 16px;
  }
  .main-title {
    font-size: 14px;
  }
  .subtitle {
    font-size: 11px;
  }
  .logo {
    width: 35px;
    height: 35px;
  }
  .counter-btn {
    padding: 6px 12px;
    font-size: 12px;
  }
}
</style> 
     