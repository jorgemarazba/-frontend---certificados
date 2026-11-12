<template>
  <div class="transfer-banner">
    <!-- Pista de trayectoria sutil y tranquila -->
    <div class="track-line">
      <div class="pulse-beam"></div>
    </div>

    <!-- ORIGEN (Izquierda): Carpeta 3D Hiperrealista -->
    <div class="endpoint origin">
      <div class="image-3d-wrapper folder-wrapper">
        <img src="@/assets/folder-3d.png" alt="Carpeta 3D" class="img-3d" />
      </div>
      <div class="endpoint-meta">
        <span class="endpoint-label">Dispositivo</span>
      </div>
    </div>

    <!-- ARCHIVO VOLANDO: 1 sola hoja de documento cada 1 minuto (Sin mareos, pausada y fluida) -->
    <div class="flying-files-container">
      <div class="flying-file" :class="tipoActual.clase">
        <div class="paper-sheet">
          <div class="corner-fold"></div>
          <div class="paper-lines">
            <span class="line line-1"></span>
            <span class="line line-2"></span>
            <span class="line line-3"></span>
          </div>
          <div class="paper-footer">
            <span class="ext-badge" :style="{ backgroundColor: tipoActual.color }">
              {{ tipoActual.extension }}
            </span>
          </div>
        </div>
      </div>
    </div>

    <!-- DESTINO (Derecha): Candado 3D Fotorrealista de Bóveda -->
    <div class="endpoint destination">
      <div class="image-3d-wrapper padlock-wrapper">
        <img src="@/assets/padlock-3d.png" alt="Candado 3D" class="img-3d" />
        <div class="lock-ring-pulse"></div>
      </div>
      <div class="endpoint-meta text-right">
        <span class="endpoint-label">Bóveda Segura</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

// Lista de tipos de documentos que se alternan elegantemente cada minuto
const tiposDoc = [
  { extension: '.PDF', color: '#dc2626', clase: 'doc-pdf' },
  { extension: '.DOCX', color: '#2563eb', clase: 'doc-docx' },
  { extension: '.XLSX', color: '#059669', clase: 'doc-xlsx' },
  { extension: '.CERT', color: '#d97706', clase: 'doc-cert' }
];

const indiceDoc = ref(0);
const tipoActual = ref(tiposDoc[0]);

let timer: any = null;

onMounted(() => {
  // Rotar el tipo de documento cada 60 segundos en sincronía exacta con la animación
  timer = setInterval(() => {
    indiceDoc.value = (indiceDoc.value + 1) % tiposDoc.length;
    tipoActual.value = tiposDoc[indiceDoc.value];
  }, 60000);
});

onUnmounted(() => {
  if (timer) clearInterval(timer);
});
</script>

<style scoped>
.transfer-banner {
  position: relative;
  width: 100%;
  height: 120px;
  background: linear-gradient(180deg, #f8fafc 0%, #edf2f9 100%);
  border-bottom: 1px solid #cbd5e1;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 48px;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.03);
}

/* Pista de trayectoria sutil */
.track-line {
  position: absolute;
  left: 150px;
  right: 150px;
  top: 50%;
  height: 2px;
  background: repeating-linear-gradient(
    90deg,
    #94a3b8 0px,
    #94a3b8 6px,
    transparent 6px,
    transparent 14px
  );
  transform: translateY(-50%);
  z-index: 1;
  opacity: 0.45;
}

/* El haz solo se activa durante el viaje de la hoja (primeros 12s de cada 60s) */
.pulse-beam {
  position: absolute;
  top: -1px;
  left: 0;
  width: 120px;
  height: 4px;
  background: linear-gradient(90deg, transparent, #16a34a, #2563eb, transparent);
  border-radius: 9999px;
  filter: blur(1px);
  animation: beamMove60s 60s infinite linear;
}

@keyframes beamMove60s {
  0%, 3% {
    left: 0%;
    opacity: 0;
  }
  5% {
    opacity: 0.9;
  }
  16% {
    opacity: 0.9;
  }
  20%, 100% {
    left: 92%;
    opacity: 0;
  }
}

/* Extremos: Origen (Carpeta) y Destino (Candado) */
.endpoint {
  position: relative;
  z-index: 5;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
}

.endpoint-meta {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.endpoint-label {
  font-size: 11px;
  font-weight: 800;
  color: #1e293b;
  letter-spacing: 0.5px;
  text-transform: uppercase;
}

.endpoint-sub {
  font-size: 10px;
  font-weight: 600;
  color: #64748b;
}

.image-3d-wrapper {
  position: relative;
  width: 76px;
  height: 76px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: transparent;
}

.img-3d {
  width: 100%;
  height: 100%;
  object-fit: contain;
  filter: drop-shadow(0 8px 16px rgba(10, 42, 94, 0.22));
  background: transparent;
}

/* CARPETA 3D: Se abre suavemente al inicio del minuto y descansa cerrada el resto */
.folder-wrapper {
  perspective: 700px;
  transform-style: preserve-3d;
  animation: folderOpenClose60s 60s cubic-bezier(0.35, 0, 0.25, 1) infinite;
}

@keyframes folderOpenClose60s {
  0% {
    /* Reposo inicial cerrada */
    transform: perspective(600px) rotateX(0deg) rotateY(0deg) scale(1);
    filter: drop-shadow(0 8px 16px rgba(10, 42, 94, 0.22));
  }
  1.5% {
    /* Se abre suavemente para liberar la hoja */
    transform: perspective(600px) rotateX(-22deg) rotateY(-16deg) scale(1.08) translateY(-3px);
    filter: drop-shadow(0 14px 22px rgba(10, 42, 94, 0.32)) brightness(1.1);
  }
  3.5% {
    /* Máxima apertura */
    transform: perspective(600px) rotateX(-18deg) rotateY(-12deg) scale(1.06) translateY(-2px);
    filter: drop-shadow(0 12px 18px rgba(10, 42, 94, 0.28)) brightness(1.08);
  }
  5% {
    /* Se cierra con calma */
    transform: perspective(600px) rotateX(2deg) rotateY(1deg) scale(0.99) translateY(0);
    filter: drop-shadow(0 6px 12px rgba(10, 42, 94, 0.22)) brightness(1);
  }
  6.5%, 100% {
    /* Completamente en reposo tranquilo durante los siguientes ~56 segundos */
    transform: perspective(600px) rotateX(0deg) rotateY(0deg) scale(1);
    filter: drop-shadow(0 8px 16px rgba(10, 42, 94, 0.22));
  }
}

/* CANDADO 3D: Reacciona suavemente cuando recibe la hoja al segundo ~12 */
.padlock-wrapper {
  position: relative;
  animation: padlockLock60s 60s ease-in-out infinite;
}

@keyframes padlockLock60s {
  0%, 18% {
    transform: scale(1);
  }
  19.5% {
    transform: scale(1.07);
    filter: drop-shadow(0 0 10px rgba(22, 163, 74, 0.6));
  }
  21% {
    transform: scale(0.98);
  }
  22.5%, 100% {
    transform: scale(1);
  }
}

.lock-ring-pulse {
  position: absolute;
  inset: -4px;
  border-radius: 16px;
  border: 2px solid #16a34a;
  opacity: 0;
  animation: ringPulse60s 60s ease-out infinite;
}

@keyframes ringPulse60s {
  0%, 18.5% {
    transform: scale(0.95);
    opacity: 0;
  }
  19.5% {
    opacity: 0.8;
    transform: scale(1.05);
  }
  21.5% {
    transform: scale(1.22);
    opacity: 0;
  }
  22%, 100% {
    transform: scale(1);
    opacity: 0;
  }
}

/* CONTENEDOR DE LA HOJA: 1 ÚNICA HOJA EN VUELO CADA MINUTO */
.flying-files-container {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 3;
}

.flying-file {
  position: absolute;
  top: 50%;
  left: 80px;
  transform: translateY(-50%);
  opacity: 0;
  /* Ciclo completo de 60 segundos (1 minuto exacto) */
  animation: flySingleDocument60s 60s cubic-bezier(0.35, 0, 0.25, 1) infinite;
}

/* DISEÑO DE LA HOJA DE PAPEL FOTORREALISTA */
.paper-sheet {
  position: relative;
  width: 44px;
  height: 56px;
  background: #ffffff;
  border-radius: 4px;
  border: 1px solid #cbd5e1;
  box-shadow: 0 8px 18px rgba(15, 23, 42, 0.16), 0 2px 4px rgba(15, 23, 42, 0.08);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 8px 6px 6px 6px;
  overflow: hidden;
}

.corner-fold {
  position: absolute;
  top: 0;
  right: 0;
  width: 13px;
  height: 13px;
  background: linear-gradient(135deg, #94a3b8 50%, #f1f5f9 50%);
  border-bottom-left-radius: 4px;
  box-shadow: -1px 1px 3px rgba(0, 0, 0, 0.18);
}

.paper-lines {
  display: flex;
  flex-direction: column;
  gap: 3px;
  margin-top: 3px;
}

.line {
  height: 2px;
  background: #cbd5e1;
  border-radius: 2px;
}

.line-1 { width: 65%; }
.line-2 { width: 85%; }
.line-3 { width: 50%; }

.paper-footer {
  display: flex;
  align-items: center;
  justify-content: center;
}

.ext-badge {
  font-size: 9px;
  font-weight: 900;
  letter-spacing: 0.5px;
  padding: 1px 4px;
  border-radius: 3px;
  color: white;
  width: 100%;
  text-align: center;
  transition: background-color 0.4s ease;
}

/* ANIMACIÓN TRANQUILA Y SERENA:
   - 0s - 1.5s: Espera en la carpeta
   - 1.5s - 3s: Asoma de la carpeta
   - 3s - 11s: Vuelo suave y relajado (sin zigzag agresivo)
   - 11s - 12.5s: Se introduce con calma en el candado 3D
   - 12.5s - 60s: REPOSO TOTAL (Total tranquilidad para el usuario)
*/
@keyframes flySingleDocument60s {
  0%, 1.2% {
    /* Dentro de la carpeta */
    left: 70px;
    transform: translateY(-46%) scale(0.2) rotate(-18deg);
    opacity: 0;
  }
  2.5% {
    /* Sale de la carpeta */
    left: 92px;
    transform: translateY(-56%) scale(0.75) rotate(-10deg);
    opacity: 0.95;
  }
  4% {
    /* Emerge hacia el aire */
    left: 130px;
    transform: translateY(-66%) scale(0.98) rotate(-4deg);
    opacity: 1;
  }
  8% {
    /* Arco suave a mitad de camino */
    transform: translateY(-62%) scale(1.01) rotate(2deg);
  }
  12% {
    /* Se estabiliza hacia la recta final */
    transform: translateY(-50%) scale(0.99) rotate(-1deg);
  }
  16.5% {
    /* Llega suavemente frente al candado */
    left: calc(100% - 170px);
    transform: translateY(-50%) scale(0.92) rotate(0deg);
    opacity: 1;
    filter: brightness(1);
  }
  18.5% {
    /* Absorción suave dentro del candado */
    left: calc(100% - 130px);
    transform: translateY(-50%) scale(0.4) rotate(12deg);
    opacity: 0.85;
    filter: brightness(1.3) drop-shadow(0 0 10px rgba(22, 163, 74, 0.8));
  }
  20% {
    /* Totalmente guardado */
    left: calc(100% - 110px);
    transform: translateY(-50%) scale(0.1) rotate(20deg);
    opacity: 0;
    filter: brightness(1.6);
  }
  20.1%, 100% {
    /* Invisible y quieto durante el resto del minuto (48 segundos en paz) */
    left: 70px;
    transform: translateY(-50%) scale(0.1);
    opacity: 0;
  }
}

/* RESPONSIVE */
@media (max-width: 768px) {
  .transfer-banner {
    padding: 0 18px;
    height: 88px;
  }
  .image-3d-wrapper {
    width: 46px;
    height: 46px;
  }
  .track-line {
    left: 70px;
    right: 70px;
  }
  .paper-sheet {
    width: 36px;
    height: 46px;
    padding: 5px 4px 4px 4px;
  }
  @keyframes flySingleDocument60s {
    0%, 1.2% {
      left: 55px;
      transform: translateY(-40%) scale(0.4);
      opacity: 0;
    }
    3% {
      opacity: 1;
    }
    16.5% {
      left: calc(100% - 95px);
      opacity: 1;
      transform: translateY(-50%) scale(0.85);
    }
    18.5% {
      left: calc(100% - 75px);
      transform: translateY(-50%) scale(0.35);
      opacity: 0.8;
    }
    20% {
      left: calc(100% - 65px);
      transform: translateY(-50%) scale(0.1);
      opacity: 0;
    }
    20.1%, 100% {
      left: 55px;
      opacity: 0;
    }
  }
}
</style>