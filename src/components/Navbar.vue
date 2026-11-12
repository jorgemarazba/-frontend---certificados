<template>
    <!-- NAVBAR-->
     <nav class="navbar">

        <!-- LADO IZQUIERDO:  logo de libro 3D animado y titulo-->
        <div class="left-section">
          <!-- Libro 3D Cohesivo y Simétrico con Animación Realista de Paso de Hojas -->
          <div class="book-3d-scene" title="Bóveda Documental">
            <div class="book-3d">
              <!-- Tapas inferiores del libro -->
              <div class="book-cover-base left-cover"></div>
              <div class="book-cover-base right-cover"></div>
              
              <!-- Página estática izquierda -->
              <div class="page-static page-left">
                <div class="page-lines">
                  <span class="pline pline-1"></span>
                  <span class="pline pline-2"></span>
                  <span class="pline pline-3"></span>
                </div>
              </div>
              
              <!-- Página estática derecha -->
              <div class="page-static page-right">
                <div class="page-lines">
                  <span class="pline pline-1"></span>
                  <span class="pline pline-2"></span>
                  <span class="pline pline-3"></span>
                </div>
              </div>

              <!-- Hoja móvil en 3D (Simetría perfecta) -->
              <div class="flipping-page-container">
                <div class="flipping-page">
                  <div class="page-side front-side">
                    <div class="page-lines">
                      <span class="pline pline-1"></span>
                      <span class="pline pline-2"></span>
                      <span class="pline pline-3"></span>
                    </div>
                  </div>
                  <div class="page-side back-side">
                    <div class="page-lines">
                      <span class="pline pline-1"></span>
                      <span class="pline pline-2"></span>
                      <span class="pline pline-3"></span>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Lomo central y Cinta dorada -->
              <div class="book-spine"></div>
              <div class="book-ribbon"></div>
            </div>
          </div>

          <div class="titles">
            <h1 class="main-title">VAULT ARCHIMENT</h1>
            <p class="subtitle">gestion documental</p>
          </div>
        </div>

    <!-- LADO DERECHO: Colaboradores, Botón contador 3D y usuario -->
    <div class="right-section">
      <!-- Botón Profesional de Colaboradores (Solo icono 2D) -->
      <button class="btn-collaborators" @click="mostrarModalColaboradores = true" title="Colaboradores">
        <svg class="collab-2d-icon" viewBox="0 0 20 20" fill="currentColor">
          <path d="M9 6a3 3 0 11-6 0 3 3 0 016 0zM17 6a3 3 0 11-6 0 3 3 0 016 0zM12.93 17c.046-.327.07-.66.07-1a6.97 6.97 0 00-1.5-4.33A5 5 0 0119 16v1h-6.07zM6 11a5 5 0 015 5v1H1v-1a5 5 0 015-5z" />
        </svg>
      </button>

      <button class="doc-icon-btn" title="Documentos guardados">
        <img src="@/assets/docs-3d.jpg" alt="Documentos" class="doc-3d-img" />
        <span class="counter-badge">{{ docCount }}</span>
      </button>

      <div class="user-avatar" title="Usuario">
        U
      </div>
    </div>
  </nav>

  <!-- MODAL PROFESIONAL: INVITAR COLABORADORES (SOLO LECTURA) -->
  <div v-if="mostrarModalColaboradores" class="collab-modal-backdrop" @click.self="mostrarModalColaboradores = false">
    <div class="collab-modal-card">
      <div class="collab-modal-header">
        <div class="header-collab-info">
          <div class="collab-badge-avatar">
            <svg class="w-6 h-6 text-blue-600" viewBox="0 0 20 20" fill="currentColor">
              <path d="M9 6a3 3 0 11-6 0 3 3 0 016 0zM17 6a3 3 0 11-6 0 3 3 0 016 0zM12.93 17c.046-.327.07-.66.07-1a6.97 6.97 0 00-1.5-4.33A5 5 0 0119 16v1h-6.07zM6 11a5 5 0 015 5v1H1v-1a5 5 0 015-5z" />
            </svg>
          </div>
          <div>
            <h3 class="collab-modal-title">Invitar Colaboradores</h3>
            <p class="collab-modal-subtitle">Comparte acceso seguro a tu espacio personal.</p>
          </div>
        </div>
        <button class="modal-close-btn" @click="mostrarModalColaboradores = false">✕</button>
      </div>

      <div class="collab-modal-body">
        <!-- Notificación de permiso SOLO LECTURA -->
        <div class="readonly-banner">
          <span class="readonly-icon">🔒</span>
          <div class="readonly-content">
            <h4 class="readonly-title">Permiso estricto de Solo Lectura</h4>
            <p class="readonly-desc">
              Los colaboradores invitados únicamente podrán <strong>visualizar y consultar</strong> tu documentación. No tendrán permisos para modificar, editar ni eliminar ningún archivo.
            </p>
          </div>
        </div>

        <!-- Formulario para invitar -->
        <div class="invite-form-group">
          <label class="form-label">Correo electrónico del invitado</label>
          <div class="invite-input-row">
            <input
              type="email"
              class="invite-input"
              placeholder="colega@ejemplo.com"
              v-model="nuevoEmail"
              @keyup.enter="invitarColaborador"
            />
            <button class="btn-send-invite" @click="invitarColaborador">
              <span>Invitar</span>
            </button>
          </div>
        </div>

        <!-- Lista de colaboradores actuales -->
        <div class="active-collabs-section">
          <div class="section-title-row">
            <span class="collab-section-title">Colaboradores con acceso</span>
            <span class="collab-total-badge">{{ colaboradoresList.length }} activos</span>
          </div>

          <div class="collab-list">
            <div v-for="(collab, idx) in colaboradoresList" :key="idx" class="collab-row-item">
              <div class="collab-profile">
                <div class="collab-avatar-circle" :style="{ backgroundColor: collab.color }">
                  {{ collab.inicial }}
                </div>
                <div>
                  <span class="collab-user-name">{{ collab.nombre }}</span>
                  <span class="collab-user-email">{{ collab.email }}</span>
                </div>
              </div>
              <span class="role-readonly-pill">
                <svg class="w-3.5 h-3.5 mr-1" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 12a2 2 0 100-4 2 2 0 000 4z" clip-rule="evenodd" />
                  <path fill-rule="evenodd" d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z" clip-rule="evenodd" />
                </svg>
                Solo Lectura
              </span>
            </div>
          </div>
        </div>
      </div>

      <div class="collab-modal-footer">
        <button class="btn-copy-share" @click="copiarEnlace">
          <span>{{ mensajeCopiado ? '✓ Enlace Copiado' : '🔗 Copiar enlace de solo lectura' }}</span>
        </button>
        <button class="btn-close-collab" @click="mostrarModalColaboradores = false">Listo</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const docCount = ref(0);

function incrementarDocumentos() {
  docCount.value++;
}

// Control de Colaboradores
const mostrarModalColaboradores = ref(false);
const nuevoEmail = ref('');
const mensajeCopiado = ref(false);

const colaboradoresList = ref([
  { nombre: 'Dra. María Gómez', email: 'maria.gomez@clinica.org', inicial: 'M', color: '#2563eb' },
  { nombre: 'Carlos Rodríguez', email: 'carlos.abogado@legal.com', inicial: 'C', color: '#7c3aed' },
]);

function invitarColaborador() {
  const email = nuevoEmail.value.trim();
  if (!email || !email.includes('@')) return;
  const username = email.split('@')[0] || 'colaborador';
  const nombre = username.charAt(0).toUpperCase() + username.slice(1);
  colaboradoresList.value.push({
    nombre: nombre,
    email: email,
    inicial: nombre.charAt(0).toUpperCase(),
    color: '#059669',
  });
  nuevoEmail.value = '';
}

function copiarEnlace() {
  navigator.clipboard.writeText(window.location.origin + '/?shared=readonly');
  mensajeCopiado.value = true;
  setTimeout(() => {
    mensajeCopiado.value = false;
  }, 2500);
}

defineExpose({ incrementarDocumentos, docCount, colaboradoresList })
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
.book-3d-scene {
  width: 52px;
  height: 38px;
  perspective: 600px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.book-3d {
  position: relative;
  width: 46px;
  height: 32px;
  transform-style: preserve-3d;
  filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.35));
}

/* Tapas del libro en la base */
.book-cover-base {
  position: absolute;
  top: 0;
  width: 50%;
  height: 100%;
  background: #0f172a;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
}
.left-cover {
  left: 0;
  border-radius: 4px 0 0 4px;
  transform: rotateY(8deg);
  transform-origin: right center;
}
.right-cover {
  right: 0;
  border-radius: 0 4px 4px 0;
  transform: rotateY(-8deg);
  transform-origin: left center;
}

/* Páginas estáticas: simétricas y con gradiente sutil de papel */
.page-static {
  position: absolute;
  top: 2px;
  width: 48%;
  height: calc(100% - 4px);
  background: linear-gradient(180deg, #ffffff 0%, #f8fafc 100%);
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 4px 5px;
  box-shadow: inset 0 0 4px rgba(0, 0, 0, 0.05);
}

.page-left {
  left: 1px;
  border-radius: 3px 0 0 3px;
  transform: rotateY(8deg);
  transform-origin: right center;
  border-right: 1px solid #e2e8f0;
}

.page-right {
  right: 1px;
  border-radius: 0 3px 3px 0;
  transform: rotateY(-8deg);
  transform-origin: left center;
  border-left: 1px solid #e2e8f0;
}

/* Líneas de texto simuladas */
.page-lines {
  display: flex;
  flex-direction: column;
  gap: 3px;
  width: 100%;
}
.pline {
  height: 2px;
  background: #cbd5e1;
  border-radius: 1px;
}
.pline-1 { width: 85%; }
.pline-2 { width: 70%; }
.pline-3 { width: 90%; }

/* Contenedor de la hoja móvil con pivote en el lomo (50%) */
.flipping-page-container {
  position: absolute;
  top: 2px;
  left: 50%;
  width: 48%;
  height: calc(100% - 4px);
  transform-style: preserve-3d;
  transform-origin: left center;
  pointer-events: none;
  animation: turnPageBook 4.6s cubic-bezier(0.4, 0.05, 0.2, 1) infinite;
}

.flipping-page {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
}

.page-side {
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, #ffffff 0%, #f8fafc 100%);
  padding: 4px 5px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  backface-visibility: hidden;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
}

.front-side {
  border-radius: 0 3px 3px 0;
  transform: rotateY(0deg);
}

.back-side {
  border-radius: 3px 0 0 3px;
  transform: rotateY(180deg);
}

/* Lomo central */
.book-spine {
  position: absolute;
  left: calc(50% - 1.5px);
  top: 0;
  width: 3px;
  height: 100%;
  background: linear-gradient(180deg, #d97706 0%, #b45309 100%);
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.3);
  z-index: 5;
}

/* Cinta marcapáginas dorada */
.book-ribbon {
  position: absolute;
  left: calc(50% - 1px);
  bottom: -4px;
  width: 2px;
  height: 8px;
  background: #f59e0b;
  box-shadow: 0 1px 2px rgba(0,0,0,0.3);
  z-index: 6;
}

/* ANIMACIÓN DE PASO DE HOJA: Simetría perfecta */
@keyframes turnPageBook {
  0%, 15% {
    /* Plana sobre la página derecha */
    transform: rotateY(-8deg);
    opacity: 0.95;
  }
  50% {
    /* En el cenit: exactamente vertical en el lomo central a 90 grados */
    transform: rotateY(-90deg) scale(1.05);
    opacity: 1;
    filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.35));
  }
  85%, 100% {
    /* Plana sobre la página izquierda de forma simétrica */
    transform: rotateY(-172deg);
    opacity: 0.95;
  }
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
  display: flex;
  align-items: center;
  gap: 16px;
}
.doc-icon-btn {
  position: relative;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.2s ease;
}
.doc-icon-btn:hover {
  transform: scale(1.08);
}
.doc-3d-img {
  width: 44px;
  height: 44px;
  object-fit: cover;
  border-radius: 10px;
  filter: drop-shadow(0 3px 6px rgba(0, 0, 0, 0.35));
}
.counter-badge {
  position: absolute;
  top: -5px;
  right: -7px;
  background-color: #16a34a;
  color: white;
  font-size: 11px;
  font-weight: 800;
  min-width: 20px;
  height: 20px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 5px;
  border: 2px solid #0A2A5E;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.25);
}
.user-avatar {
  width: 38px;
  height: 38px;
  background-color: #1e40af;
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.8);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 15px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
}

/* BOTÓN PROFESIONAL COLABORADORES EN NAVBAR (SOLO ICONO 2D) */
.btn-collaborators {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.12);
  border: 1px solid rgba(255, 255, 255, 0.25);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  cursor: pointer;
  backdrop-filter: blur(8px);
  transition: all 0.2s ease;
  padding: 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.btn-collaborators:hover {
  background: rgba(255, 255, 255, 0.25);
  transform: scale(1.08);
  border-color: rgba(255, 255, 255, 0.45);
}

.collab-2d-icon {
  width: 20px;
  height: 20px;
  fill: currentColor;
}

/* MODAL DE COLABORADORES */
.collab-modal-backdrop {
  position: fixed;
  inset: 0;
  background: rgba(15, 23, 42, 0.65);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 200;
  padding: 20px;
}

.collab-modal-card {
  background: white;
  border-radius: 16px;
  width: 100%;
  max-width: 520px;
  color: #1e293b;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.3);
  overflow: hidden;
  animation: collabModalEnter 0.2s ease-out;
}

@keyframes collabModalEnter {
  from { opacity: 0; transform: scale(0.95); }
  to { opacity: 1; transform: scale(1); }
}

.collab-modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 18px 24px;
  background: #f8fafc;
  border-bottom: 1px solid #e2e8f0;
}

.header-collab-info {
  display: flex;
  align-items: center;
  gap: 12px;
}

.collab-badge-avatar {
  width: 40px;
  height: 40px;
  background: #dbeafe;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.collab-modal-title {
  font-size: 17px;
  font-weight: 800;
  color: #0A2A5E;
  margin: 0;
}

.collab-modal-subtitle {
  font-size: 12px;
  color: #64748b;
  margin: 2px 0 0 0;
}

.modal-close-btn {
  background: transparent;
  border: none;
  font-size: 16px;
  color: #64748b;
  cursor: pointer;
  padding: 6px;
  border-radius: 6px;
}

.modal-close-btn:hover {
  background: #e2e8f0;
}

.collab-modal-body {
  padding: 20px 24px;
  display: flex;
  flex-direction: column;
  gap: 18px;
}

/* BANNER DE SOLO LECTURA */
.readonly-banner {
  background: #f0fdf4;
  border: 1px solid #bbf7d0;
  border-radius: 10px;
  padding: 12px 14px;
  display: flex;
  gap: 10px;
  align-items: flex-start;
}

.readonly-icon {
  font-size: 18px;
  flex-shrink: 0;
}

.readonly-title {
  font-size: 13px;
  font-weight: 800;
  color: #15803d;
  margin: 0 0 2px 0;
}

.readonly-desc {
  font-size: 12px;
  color: #166534;
  margin: 0;
  line-height: 1.4;
}

.invite-form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-label {
  font-size: 12.5px;
  font-weight: 700;
  color: #334155;
}

.invite-input-row {
  display: flex;
  gap: 8px;
}

.invite-input {
  flex: 1;
  padding: 10px 14px;
  border: 1.5px solid #e2e8f0;
  border-radius: 8px;
  font-size: 13.5px;
  outline: none;
  background: #f8fafc;
  color: #0f172a;
}

.invite-input:focus {
  background: white;
  border-color: #2563eb;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.15);
}

.btn-send-invite {
  background: #0A2A5E;
  color: white;
  border: none;
  padding: 10px 18px;
  border-radius: 8px;
  font-size: 13px;
  font-weight: 700;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.btn-send-invite:hover {
  background: #1e3a8a;
}

.active-collabs-section {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.section-title-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.collab-section-title {
  font-size: 12.5px;
  font-weight: 700;
  color: #475569;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.collab-total-badge {
  font-size: 11px;
  font-weight: 700;
  background: #f1f5f9;
  color: #64748b;
  padding: 2px 8px;
  border-radius: 12px;
}

.collab-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
  max-height: 180px;
  overflow-y: auto;
}

.collab-row-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px 12px;
  background: #f8fafc;
  border: 1px solid #f1f5f9;
  border-radius: 8px;
}

.collab-profile {
  display: flex;
  align-items: center;
  gap: 10px;
}

.collab-avatar-circle {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  color: white;
  font-weight: 800;
  font-size: 13px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.collab-user-name {
  font-size: 13px;
  font-weight: 700;
  color: #1e293b;
  display: block;
}

.collab-user-email {
  font-size: 11px;
  color: #64748b;
  display: block;
}

.role-readonly-pill {
  font-size: 11px;
  font-weight: 700;
  color: #0369a1;
  background: #e0f2fe;
  padding: 3px 8px;
  border-radius: 20px;
  display: inline-flex;
  align-items: center;
}

.collab-modal-footer {
  padding: 14px 24px;
  background: #f8fafc;
  border-top: 1px solid #e2e8f0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.btn-copy-share {
  background: white;
  border: 1px solid #cbd5e1;
  color: #334155;
  padding: 8px 14px;
  border-radius: 8px;
  font-size: 12.5px;
  font-weight: 700;
  cursor: pointer;
}

.btn-copy-share:hover {
  background: #f1f5f9;
}

.btn-close-collab {
  background: #0A2A5E;
  color: white;
  border: none;
  padding: 8px 18px;
  border-radius: 8px;
  font-size: 13px;
  font-weight: 700;
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
  .book-3d-scene {
    width: 44px;
    height: 32px;
  }
  .book-3d {
    width: 38px;
    height: 26px;
  }
  .doc-3d-img {
    width: 36px;
    height: 36px;
  }
}
</style> 
     