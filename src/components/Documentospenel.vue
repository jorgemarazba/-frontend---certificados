<template>
  <div class="container">
    
    <!-- Titulo verdecito -->
    <h2 class="title-green">Documentos</h2>
    <p class="subtitle">Un lugar ordenado para cada documento personal.</p>

    <button class="btn-green" @click="guardados++">
      <span class="plus">+</span> Adjuntar documento
    </button>

    <!-- Cuadro stats -->
    <div class="stats-card">
      <div class="stats-top">
        <div class="stat-item">
          <div class="stat-header">
            <span class="icon">📄</span>
            <span class="stat-label">Documentos guardados</span>
          </div>
          <span class="stat-number">{{ guardados }}</span>
        </div>
        <div class="stat-item">
          <div class="stat-header">
            <span class="icon">🕒</span>
            <span class="stat-label">Pendientes en revisión</span>
          </div>
          <span class="stat-number">{{ pendientes }}</span>
        </div>
      </div>
      <hr class="divider" />
      <div class="secure-line">
        <span class="shield">🛡️<span class="check">✔</span></span>
        <span class="secure-text">Se guardan de forma segura en este dispositivo</span>
      </div>
    </div>

    <!-- NUEVO BLOQUE DEBAJO -->
    <h2 class="organiza-title">Organiza y consulta y actualiza tu documentación.</h2>

    <div class="search-bar">
      <span class="search-icon">🔍</span>
      <input type="text" placeholder="Buscar por nombre..." v-model="busqueda" />
    </div>

    <div class="filters">
      <span class="filter-label">⚙️ Filtrar</span>
      <select class="dropdown">
        <option>Todos los estados</option>
        <option>Guardado</option>
        <option>Pendiente</option>
      </select>
      <select class="dropdown">
        <option>Todos los tipos</option>
        <option>Certificado</option>
        <option>Identidad</option>
      </select>
    </div>

    <div class="table-container">
      <table class="docs-table">
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Tipo de documento</th>
            <th>Tipo de documento</th>
            <th>Fecha</th>
            <th>Estado</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(doc, i) in documentos" :key="i">
            <td>{{ doc.nombre }}</td>
            <td>{{ doc.tipo }}</td>
            <td>{{ doc.tipo }}</td>
            <td>{{ doc.fecha }}</td>
            <td><span class="badge">{{ doc.estado }}</span></td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

// ESTAS SON LAS VARIABLES QUE TE FALTABAN - Linea 95 a 105
const guardados = ref(3);
const pendientes = ref(1);
const busqueda = ref('');

const documentos = ref([
  { nombre: 'Certificado EPS', tipo: 'Certificado', fecha: '20/10/2025', estado: 'Guardado' },
  { nombre: 'Cedula', tipo: 'Identidad', fecha: '18/10/2025', estado: 'Pendiente' },
  { nombre: 'Diploma Universidad', tipo: 'Certificado', fecha: '15/10/2025', estado: 'Aprobado' },
]);
</script>

<style scoped>
.container { padding: 24px; max-width: 700px; }
.title-green { color: #16a34a; font-size: 28px; font-weight: 700; margin: 0; }
.subtitle { color: #4b5563; font-size: 15px; margin: 6px 0 20px 0; }
.btn-green { background: #16a34a; color: white; border: none; padding: 10px 18px; border-radius: 8px; font-weight: 600; cursor: pointer; display: flex; gap: 8px; margin-bottom: 24px; }
.plus { font-size: 18px; font-weight: bold; }
.stats-card { background: white; border: 1px solid #e5e7eb; border-radius: 12px; padding: 20px; }
.stats-top { display: flex; justify-content: space-between; }
.stat-item { display: flex; flex-direction: column; }
.stat-header { display: flex; align-items: center; gap: 6px; }
.stat-label { font-size: 12px; color: #6b7280; }
.stat-number { font-size: 22px; font-weight: 700; margin: 4px 0 0 24px; }
.divider { border: none; border-top: 1px solid #e5e7eb; margin: 16px 0; }
.secure-line { display: flex; align-items: center; gap: 8px; }
.shield { position: relative; font-size: 18px; }
.check { color: #16a34a; font-size: 12px; position: absolute; bottom: -2px; right: -4px; background: white; border-radius: 50%; }
.secure-text { font-size: 13px; color: #374151; }
.organiza-title { font-size: 20px; font-weight: 700; color: #111827; margin: 40px 0 16px 0; }
.search-bar { background: white; border: 1px solid #e5e7eb; border-radius: 8px; display: flex; align-items: center; padding: 10px 14px; gap: 8px; margin-bottom: 16px; }
.search-bar input { border: none; outline: none; width: 100%; font-size: 14px; }
.filters { display: flex; align-items: center; gap: 12px; margin-bottom: 20px; }
.filter-label { font-size: 14px; font-weight: 600; }
.dropdown { border: 1px solid #e5e7eb; border-radius: 6px; padding: 6px 10px; font-size: 13px; background: white; }
.table-container { background: white; border-radius: 10px; border: 1px solid #e5e7eb; overflow: hidden; }
.docs-table { width: 100%; border-collapse: collapse; }
.docs-table thead { background: #f3f4f6; }
.docs-table th { text-align: left; font-size: 12px; color: #6b7280; font-weight: 600; padding: 12px 16px; text-transform: uppercase; }
.docs-table td { padding: 12px 16px; font-size: 14px; border-top: 1px solid #e5e7eb; }
.badge { background: #dcfce7; color: #16a34a; padding: 3px 8px; border-radius: 12px; font-size: 12px; }

/* RESPONSIVE PANEL */
@media (max-width: 768px) {
  .container {
    padding: 16px;
    max-width: 100%;
  }
  .title-green {
    font-size: 22px;
  }
  .stats-top {
    flex-direction: column;
    gap: 16px;
  }
  .filters {
    flex-direction: column;
    align-items: stretch;
  }
  .dropdown {
    width: 100%;
  }
  .table-container {
    overflow-x: auto; /* La tabla se puede deslizar con el dedo */
  }
  .docs-table {
    min-width: 500px;
  }
  .organiza-title {
    font-size: 16px;
    line-height: 1.3;
  }
}

/* Para tablets */
@media (min-width: 769px) and (max-width: 1024px) {
  .container {
    max-width: 90%;
  }
}
</style>