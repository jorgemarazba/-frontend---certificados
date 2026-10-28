<template>
    <!--recuadro blanco--->
    <div class="workspace-bar">

        <!-- Linea 5: LADO IZQUIERDO -->
         <div class="left">
           
            <!-- Titulo 1 -->
             <span class="label">espacio de trabajo</span> 

             <!-- Linea 9: Flecha señalando -->
      <span class="arrow">→</span>
      <!-- Titulo 2 -->
      <span class="docs">Documentos</span>
    </div>

    <!-- Linea 15: LADO DERECHO - Logo usuario -->
    <div class="right">
      <div class="user-logo">
        <!-- Puedes poner una letra o inicial -->
        U
      </div>
    </div>

  </div>
</template>

<script setup lang="ts">
// Linea 27: Aqui por ahora no necesitamos logica
</script>

<style scoped>
/* Linea 31: El recuadro blanco */
.workspace-bar {
  background-color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 24px;
  border-bottom: 1px solid #e5e7eb;
  box-shadow: 0 1px 3px rgba(0,0,0,0.05);
}
.left {
  display: flex;
  align-items: center;
  gap: 8px;
}
.label {
  color: #6b7280;
  font-size: 14px;
  text-transform: lowercase;
}
.arrow {
  color: #9ca3af;
  font-size: 14px;
}
.docs {
  color: #111827;
  font-weight: 600;
  font-size: 14px;
}
.right {
}
.user-logo {
  width: 36px;
  height: 36px;
  background-color: #0A2A5E; /* Mismo azul del navbar */
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}

@media (max-width: 768px) {
  .workspace-bar {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
    padding: 10px 16px;
  }
  .right {
    align-self: flex-end;
    position: absolute;
    right: 16px;
    top: 82px;
  }
}
</style>