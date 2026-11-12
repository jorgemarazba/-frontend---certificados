<template>
  <div class="container">

    <div class="dashboard-layout">
      <!-- COLUMNA IZQUIERDA: Panel de Estadísticas y Gráficos 3D Pegado a la Izquierda -->
      <aside class="stats-sidebar">
        <div class="stats-card">
          
          <!-- Encabezado de Métricas de Bóveda -->
          <div class="stats-card-header">
            <div>
              <h3 class="stats-card-title">Métricas de Bóveda</h3>
              <p class="stats-card-subtitle">Análisis en tiempo real</p>
            </div>
          </div>

          <!-- GRÁFICO 3D: Barras Isométricas con Espaciado Generoso -->
          <div class="bar-chart-3d-box">
            <div class="bar-chart-header">
              <span class="bar-chart-title">Volumen por categoría</span>
              <span class="bar-chart-tag">En vivo</span>
            </div>

            <div class="bars-isometric-container">
              <!-- Barra 1: Guardados -->
              <div class="iso-bar-col">
                <div class="iso-bar bar-green" :style="{ height: getBarHeight(guardados) }">
                  <span class="iso-top"></span>
                  <span class="iso-val">{{ guardados }}</span>
                </div>
                <span class="iso-lbl">Guard.</span>
              </div>

              <!-- Barra 2: Pendientes -->
              <div class="iso-bar-col">
                <div class="iso-bar bar-amber" :style="{ height: getBarHeight(pendientes) }">
                  <span class="iso-top"></span>
                  <span class="iso-val">{{ pendientes }}</span>
                </div>
                <span class="iso-lbl">Pend.</span>
              </div>

              <!-- Barra 3: Enviados -->
              <div class="iso-bar-col">
                <div class="iso-bar bar-blue" :style="{ height: getBarHeight(enviados) }">
                  <span class="iso-top"></span>
                  <span class="iso-val">{{ enviados }}</span>
                </div>
                <span class="iso-lbl">Env.</span>
              </div>

              <!-- Barra 4: Colaboradores -->
              <div class="iso-bar-col">
                <div class="iso-bar bar-purple" :style="{ height: getBarHeight(colaboradores) }">
                  <span class="iso-top"></span>
                  <span class="iso-val">{{ colaboradores }}</span>
                </div>
                <span class="iso-lbl">Colab.</span>
              </div>
            </div>
          </div>

          <!-- LISTA DE MÉTRICAS CON ICONOS REALISTAS SVG Y RELIEVE -->
          <div class="stats-list">
            <!-- Defs comunes para gradientes de iconos -->
            <svg class="hidden-defs" width="0" height="0">
              <defs>
                <linearGradient id="doc-grad" x1="0%" y1="0%" x2="100%" y2="100%">
                  <stop offset="0%" stop-color="#ffffff" />
                  <stop offset="100%" stop-color="#dcfce7" />
                </linearGradient>
                <linearGradient id="clock-grad" x1="0%" y1="0%" x2="100%" y2="100%">
                  <stop offset="0%" stop-color="#fffbeb" />
                  <stop offset="100%" stop-color="#fef3c7" />
                </linearGradient>
                <linearGradient id="send-grad" x1="0%" y1="0%" x2="100%" y2="100%">
                  <stop offset="0%" stop-color="#bfdbfe" />
                  <stop offset="100%" stop-color="#3b82f6" />
                </linearGradient>
                <linearGradient id="trash-grad" x1="0%" y1="0%" x2="100%" y2="100%">
                  <stop offset="0%" stop-color="#ffffff" />
                  <stop offset="100%" stop-color="#fee2e2" />
                </linearGradient>
                <linearGradient id="team-grad1" x1="0%" y1="0%" x2="100%" y2="100%">
                  <stop offset="0%" stop-color="#faf5ff" />
                  <stop offset="100%" stop-color="#e9d5ff" />
                </linearGradient>
              </defs>
            </svg>

            <!-- 1. Documentos guardados -->
            <div class="stat-item item-green">
              <div class="stat-left">
                <div class="stat-icon-3d icon-docs">
                  <svg class="realistic-svg" viewBox="0 0 24 24" fill="none">
                    <path d="M6 2C4.89 2 4 2.89 4 4V20C4 21.1 4.89 22 6 22H18C19.1 22 20 21.1 20 20V8L14 2H6Z" fill="url(#doc-grad)" stroke="#16a34a" stroke-width="1.3" />
                    <path d="M14 2V8H20L14 2Z" fill="#86efac" />
                    <line x1="8" y1="12" x2="16" y2="12" stroke="#15803d" stroke-width="1.6" stroke-linecap="round"/>
                    <line x1="8" y1="16" x2="13" y2="16" stroke="#15803d" stroke-width="1.6" stroke-linecap="round"/>
                  </svg>
                </div>
                <div>
                  <span class="stat-label">Documentos guardados</span>
                  <div class="stat-progress-bg">
                    <div class="stat-progress-fill fill-green" :style="{ width: Math.min(100, guardados * 25) + '%' }"></div>
                  </div>
                </div>
              </div>
              <span class="stat-number num-green">{{ guardados }}</span>
            </div>

            <!-- 2. Pendientes en revisión -->
            <div class="stat-item item-amber">
              <div class="stat-left">
                <div class="stat-icon-3d icon-pending">
                  <svg class="realistic-svg" viewBox="0 0 24 24" fill="none">
                    <circle cx="12" cy="12" r="9" fill="url(#clock-grad)" stroke="#d97706" stroke-width="1.4" />
                    <circle cx="12" cy="12" r="7.5" stroke="#fef3c7" stroke-width="0.8" />
                    <path d="M12 7V12L15.5 14" stroke="#78350f" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <circle cx="12" cy="12" r="1.3" fill="#78350f" />
                  </svg>
                </div>
                <div>
                  <span class="stat-label">Pendientes en revisión</span>
                  <div class="stat-progress-bg">
                    <div class="stat-progress-fill fill-amber" :style="{ width: Math.min(100, pendientes * 35) + '%' }"></div>
                  </div>
                </div>
              </div>
              <span class="stat-number num-amber">{{ pendientes }}</span>
            </div>

            <!-- 3. Documentos enviados -->
            <div class="stat-item item-blue">
              <div class="stat-left">
                <div class="stat-icon-3d icon-sent">
                  <svg class="realistic-svg" viewBox="0 0 24 24" fill="none">
                    <path d="M22 2L11 13" stroke="#1d4ed8" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M22 2L15 22L11 13L2 9L22 2Z" fill="url(#send-grad)" stroke="#1e40af" stroke-width="1.3" stroke-linejoin="round"/>
                  </svg>
                </div>
                <div>
                  <span class="stat-label">Documentos enviados</span>
                  <div class="stat-progress-bg">
                    <div class="stat-progress-fill fill-blue" :style="{ width: Math.min(100, enviados * 20) + '%' }"></div>
                  </div>
                </div>
              </div>
              <span class="stat-number num-blue">{{ enviados }}</span>
            </div>

            <!-- 4. Eliminados -->
            <div class="stat-item item-red">
              <div class="stat-left">
                <div class="stat-icon-3d icon-deleted">
                  <svg class="realistic-svg" viewBox="0 0 24 24" fill="none">
                    <path d="M4 7H20M10 11V17M14 11V17M5 7L6 19C6 20.1 6.9 21 8 21H16C17.1 21 18 20.1 18 19L19 7M9 7V4C9 3.4 9.4 3 10 3H14C14.6 3 15 3.4 15 4V7" stroke="#dc2626" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" fill="url(#trash-grad)"/>
                  </svg>
                </div>
                <div>
                  <span class="stat-label">Eliminados</span>
                  <div class="stat-progress-bg">
                    <div class="stat-progress-fill fill-red" :style="{ width: Math.min(100, eliminados * 20) + '%' }"></div>
                  </div>
                </div>
              </div>
              <span class="stat-number num-red">{{ eliminados }}</span>
            </div>

            <!-- 5. Mis colaboradores -->
            <div class="stat-item item-purple">
              <div class="stat-left">
                <div class="stat-icon-3d icon-team">
                  <svg class="realistic-svg" viewBox="0 0 24 24" fill="none">
                    <circle cx="9" cy="8" r="3.8" fill="url(#team-grad1)" stroke="#7e22ce" stroke-width="1.2"/>
                    <path d="M2 19C2 15.7 5.1 13 9 13C12.9 13 16 15.7 16 19" stroke="#7e22ce" stroke-width="1.6" stroke-linecap="round" fill="url(#team-grad1)"/>
                    <circle cx="16.5" cy="8.5" r="2.8" fill="#f3e8ff" stroke="#9333ea" stroke-width="1"/>
                    <path d="M15.5 15C17.2 15.8 18.5 17.2 18.5 19" stroke="#9333ea" stroke-width="1.3" stroke-linecap="round"/>
                  </svg>
                </div>
                <div>
                  <span class="stat-label">Mis colaboradores</span>
                  <div class="stat-progress-bg">
                    <div class="stat-progress-fill fill-purple" :style="{ width: Math.min(100, colaboradores * 30) + '%' }"></div>
                  </div>
                </div>
              </div>
              <span class="stat-number num-purple">{{ colaboradores }}</span>
            </div>
          </div>

          <hr class="divider" />
          
          <div class="secure-line">
            <span class="shield">🛡️<span class="check">✔</span></span>
            <span class="secure-text">Cifrado de grado bancario activo en este dispositivo</span>
          </div>
        </div>
      </aside>

      <!-- COLUMNA DERECHA: Búsqueda, Filtros Profesionales y Tabla con Acciones -->
      <main class="main-content">
        <!-- Barra de acción superior -->
        <div class="content-header-row">
          <div>
            <h2 class="organiza-title">Organiza, consulta y actualiza tu documentación</h2>
            <p class="organiza-subtitle">Gestión centralizada de certificados y documentos oficiales.</p>
          </div>
          <button class="btn-green-action" @click="abrirModalNuevo">
            <svg class="w-5 h-5 mr-1" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd" />
            </svg>
            <span>Adjuntar documento</span>
          </button>
        </div>

        <!-- PANEL DE CONTROL: Buscador y Filtros Profesionales -->
        <div class="control-panel-card">
          <!-- Buscador elegante -->
          <div class="search-box-pro">
            <svg class="search-icon-svg" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd" />
            </svg>
            <input
              type="text"
              class="search-input-pro"
              placeholder="Buscar documento por nombre, tipo o fecha..."
              v-model="busqueda"
            />
            <button v-if="busqueda" class="clear-search-btn" @click="busqueda = ''" title="Limpiar búsqueda">✕</button>
          </div>

          <!-- Filtros estilizados con iconos -->
          <div class="filter-controls-pro">
            <div class="filter-label-group">
              <svg class="filter-icon-svg" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M3 3a1 1 0 011-1h12a1 1 0 011 1v3a1 1 0 01-.293.707L12 11.414V15a1 1 0 01-.293.707l-2 2A1 1 0 018 17v-5.586L3.293 6.707A1 1 0 013 6V3z" clip-rule="evenodd" />
              </svg>
              <span class="filter-title">Filtrar:</span>
            </div>

            <!-- Selector de Estado -->
            <div class="select-wrapper">
              <select class="dropdown-pro" v-model="estadoFiltro">
                <option value="">Todos los estados</option>
                <option value="Guardado">Guardado</option>
                <option value="Pendiente">Pendiente</option>
                <option value="Aprobado">Aprobado</option>
              </select>
            </div>

            <!-- Selector de Tipo -->
            <div class="select-wrapper">
              <select class="dropdown-pro" v-model="tipoFiltro">
                <option value="">Todos los tipos</option>
                <option value="Certificado">Certificado</option>
                <option value="Identidad">Identidad</option>
                <option value="Diploma">Diploma</option>
              </select>
            </div>

            <!-- Contador de registros filtrados -->
            <span class="results-badge">
              {{ documentosFiltrados.length }} {{ documentosFiltrados.length === 1 ? 'resultado' : 'resultados' }}
            </span>
          </div>
        </div>

        <!-- TABLA PROFESIONAL SIN ICONOS EN COLUMNA DOCUMENTO -->
        <div class="table-container-pro">
          <table class="docs-table-pro">
            <thead>
              <tr>
                <th>DOCUMENTO</th>
                <th>TIPO</th>
                <th>FECHA DE EMISIÓN</th>
                <th>ESTADO</th>
                <th class="th-actions">ACCIONES</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(doc, i) in documentosPaginados" :key="doc.id || i" class="table-row-pro">
                <!-- Documento SIN iconos (limpio) -->
                <td class="td-doc-name">
                  <span class="doc-text-name">{{ doc.nombre }}</span>
                </td>

                <!-- Tipo -->
                <td>
                  <span class="type-pill">{{ doc.tipo }}</span>
                </td>

                <!-- Fecha -->
                <td class="td-date">{{ doc.fecha }}</td>

                <!-- Estado con badges de color -->
                <td>
                  <span :class="['status-badge', getStatusClass(doc.estado)]">
                    <span class="status-dot"></span>
                    {{ doc.estado }}
                  </span>
                </td>

                <!-- BOTONES DE ACCIONES (SOLO ICONOS) -->
                <td class="td-actions">
                  <div class="actions-group">
                    <!-- BOTÓN VISUALIZAR DOCUMENTO (TAMAÑO A4) -->
                    <button
                      class="btn-action-icon btn-view-icon"
                      @click="abrirVisualizar(doc)"
                      title="Visualizar documento en tamaño A4 completo"
                    >
                      <svg class="w-4 h-4" viewBox="0 0 20 20" fill="currentColor">
                        <path d="M10 12a2 2 0 100-4 2 2 0 000 4z" />
                        <path fill-rule="evenodd" d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z" clip-rule="evenodd" />
                      </svg>
                    </button>

                    <button
                      class="btn-action-icon btn-edit-icon"
                      @click="abrirEditar(doc)"
                      title="Editar y gestionar documento"
                    >
                      <svg class="w-4 h-4" viewBox="0 0 20 20" fill="currentColor">
                        <path d="M13.586 3.586a2 2 0 112.828 2.828l-.793.793-2.828-2.828.793-.793zM11.379 5.793L3 14.172V17h2.828l8.38-8.379-2.83-2.828z" />
                      </svg>
                    </button>

                    <button
                      class="btn-action-icon btn-delete-icon"
                      @click="eliminarDoc(doc)"
                      title="Eliminar este documento"
                    >
                      <svg class="w-4 h-4" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
                      </svg>
                    </button>
                  </div>
                </td>
              </tr>

              <!-- Estado vacío cuando no hay coincidencias -->
              <tr v-if="documentosFiltrados.length === 0">
                <td colspan="5" class="empty-state-cell">
                  <div class="empty-state-box">
                    <span class="empty-icon">📂</span>
                    <p class="empty-title">No se encontraron documentos</p>
                    <p class="empty-sub">Intenta ajustar tu búsqueda o los filtros seleccionados.</p>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>

          <!-- BARRA DE PAGINACIÓN PROFESIONAL -->
          <div class="pagination-container-pro" v-if="documentosFiltrados.length > 0">
            <!-- Información de rango -->
            <div class="pagination-info">
              <span>Mostrando</span>
              <span class="pagination-highlight">{{ indiceInicio + 1 }} - {{ Math.min(indiceFin, documentosFiltrados.length) }}</span>
              <span>de</span>
              <span class="pagination-highlight">{{ documentosFiltrados.length }}</span>
              <span>documentos</span>
            </div>

            <!-- Selector de cantidad por página -->
            <div class="pagination-size-selector">
              <span class="size-label">Filas por página:</span>
              <select v-model="itemsPorPagina" class="select-per-page" @change="cambiarItemsPorPagina">
                <option :value="3">3</option>
                <option :value="5">5</option>
                <option :value="10">10</option>
              </select>
            </div>

            <!-- Controles de navegación y números -->
            <div class="pagination-controls">
              <!-- Botón Anterior -->
              <button
                class="btn-page-nav"
                :disabled="paginaActual === 1"
                @click="irAPagina(paginaActual - 1)"
                title="Página anterior"
              >
                ‹ Anterior
              </button>

              <!-- Números de página -->
              <div class="page-numbers-group">
                <button
                  v-for="pag in totalPaginas"
                  :key="pag"
                  :class="['btn-page-number', paginaActual === pag ? 'page-active' : '']"
                  @click="irAPagina(pag)"
                >
                  {{ pag }}
                </button>
              </div>

              <!-- Botón Siguiente -->
              <button
                class="btn-page-nav"
                :disabled="paginaActual === totalPaginas"
                @click="irAPagina(paginaActual + 1)"
                title="Página siguiente"
              >
                Siguiente ›
              </button>
            </div>
          </div>
        </div>
      </main>
    </div>

    <!-- MODAL PROFESIONAL: VISUALIZADOR DE DOCUMENTO EN FORMATO A4 COMPLETO -->
    <div v-if="mostrarModalVisualizar && docVisualizando" class="modal-backdrop modal-a4-backdrop" @click.self="mostrarModalVisualizar = false">
      <div class="a4-viewer-container">
        <!-- Barra superior flotante de acciones del visor A4 -->
        <div class="a4-viewer-header">
          <div class="a4-header-left">
            <span class="a4-doc-badge">DOCUMENTO OFICIAL A4</span>
            <span class="a4-doc-title">{{ docVisualizando.nombre }}</span>
            <span :class="['status-badge', getStatusClass(docVisualizando.estado)]">
              <span class="status-dot"></span>
              {{ docVisualizando.estado }}
            </span>
          </div>
          <div class="a4-header-actions">
            <button class="btn-a4-action" @click="imprimirDocumento" title="Imprimir documento">
              <svg class="w-4 h-4 mr-1.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 17h2a2 2 0 002-2v-4a2 2 0 00-2-2H5a2 2 0 00-2 2v4a2 2 0 002 2h2m2 4h6a2 2 0 002-2v-4a2 2 0 00-2-2H9a2 2 0 00-2 2v4a2 2 0 002 2zm8-12V5a2 2 0 00-2-2H9a2 2 0 00-2 2v4h10z" />
              </svg>
              <span>Imprimir</span>
            </button>
            <button class="a4-close-btn" @click="mostrarModalVisualizar = false" title="Cerrar visor">✕</button>
          </div>
        </div>

        <!-- Área de desplazamiento del pliego A4 -->
        <div class="a4-sheet-scroll-area">
          <!-- HOJA REALISTA CON DIMENSIONES Y PROPORCIONES A4 (1 : 1.414) -->
          <div class="a4-paper-page">
            <!-- Marca de agua de seguridad -->
            <div class="a4-watermark">VAULT ARCHIMENT</div>

            <!-- Membrete oficial -->
            <div class="a4-official-header">
              <div class="a4-header-emblem">
                <div class="a4-emblem-circle">
                  <span>🏛️</span>
                </div>
                <div class="a4-emblem-text">
                  <span class="a4-gov-title">SISTEMA DE GESTIÓN DOCUMENTAL Y CUSTODIA</span>
                  <span class="a4-gov-sub">BÓVEDA DIGITAL DE SEGURIDAD JURÍDICA</span>
                </div>
              </div>
              <div class="a4-folio-box">
                <span class="a4-folio-label">FOLIO ELECTRÓNICO</span>
                <span class="a4-folio-val">VA-{{ docVisualizando.id || '2026' }}-{{ String(docVisualizando.fecha).replace(/\//g, '') }}</span>
                <span class="a4-date-stamp">Expedición: {{ docVisualizando.fecha }}</span>
              </div>
            </div>

            <div class="a4-divider-double"></div>

            <!-- Título central del documento -->
            <div class="a4-title-section">
              <span class="a4-type-badge">{{ docVisualizando.tipo.toUpperCase() }}</span>
              <h1 class="a4-main-heading">{{ docVisualizando.nombre }}</h1>
              <span class="a4-status-declaration">DOCUMENTO REGISTRADO EN BÓVEDA CON VALIDEZ Y EFECTOS LEGALES</span>
            </div>

            <!-- Cuerpo del texto completo -->
            <div class="a4-content-body">
              <p v-for="(parrafo, pIdx) in (docVisualizando.texto || '').split('\n\n')" :key="pIdx" class="a4-paragraph">
                {{ parrafo }}
              </p>
            </div>

            <!-- Archivo digital adjunto en caso de existir -->
            <div v-if="docVisualizando.archivo" class="a4-attached-meta">
              <div class="a4-attached-left">
                <span class="a4-attached-icon">📎</span>
                <div>
                  <span class="a4-attached-name">Archivo Digital Respaldado: {{ docVisualizando.archivo.nombre }}</span>
                  <span class="a4-attached-source">{{ docVisualizando.archivo.origen === 'local' ? '📁 Almacenamiento Local Cifrado' : '🌐 Repositorio Remoto Vinculado' }}</span>
                </div>
              </div>
              <span class="a4-hash-badge">SHA-256: 8f4a7c...39b2</span>
            </div>

            <!-- Pie de página A4 con sello digital y firmas -->
            <div class="a4-official-footer">
              <div class="a4-signature-box">
                <div class="a4-signature-line"></div>
                <span class="a4-sign-name">DIRECCIÓN GENERAL DE ARCHIVO Y CUSTODIA</span>
                <span class="a4-sign-role">Bóveda Documental Certificada</span>
              </div>

              <!-- Sello QR / Seguridad -->
              <div class="a4-seal-box">
                <div class="a4-qr-mock">
                  <div class="qr-pattern"></div>
                  <span class="qr-text">VERIFICADO</span>
                </div>
                <div class="a4-seal-text">
                  <span>SEGURIDAD CRIPTOGRÁFICA</span>
                  <span class="text-xs text-emerald-700 font-bold">✓ DOCUMENTO AUTÉNTICO</span>
                </div>
              </div>
            </div>

            <!-- Pie de página final -->
            <div class="a4-bottom-page-number">
              <span>Página 1 de 1 • Vault Archiment Document Vault • Uso confidencial y exclusivo del titular</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- MODAL PROFESIONAL AVANZADO: EDITAR DOCUMENTO EN 3D (LOCAL/WEB Y EDITOR WORD) -->
    <div v-if="mostrarModalEditar" class="modal-backdrop" @click.self="mostrarModalEditar = false">
      <div class="modal-card modal-wide modal-3d-container">
        <!-- Encabezado 3D del Modal con pestañas táctiles -->
        <div class="modal-header modal-3d-header">
          <div class="modal-3d-brand">
            <div class="modal-3d-icon-badge">
              <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
              </svg>
            </div>
            <div>
              <h3 class="modal-3d-title">Editar Documento</h3>
              <span class="modal-3d-doc-tag">{{ docEdicion.nombre || 'Documento de Bóveda' }}</span>
            </div>
          </div>

          <div class="modal-3d-tabs">
            <button
              :class="['modal-3d-tab-btn', tabActiva === 'info' ? 'tab-3d-active' : '']"
              @click="tabActiva = 'info'"
            >
              <span>⚙️ Metadatos y Archivos</span>
            </button>
            <button
              :class="['modal-3d-tab-btn', tabActiva === 'word' ? 'tab-3d-active' : '']"
              @click="tabActiva = 'word'"
            >
              <span>📝 Editor Word 3D</span>
            </button>
          </div>

          <button class="modal-close-btn-pro" @click="mostrarModalEditar = false" title="Cerrar ventana">✕</button>
        </div>

        <div class="modal-body modal-3d-body">
          <!-- PESTAÑA 1: METADATOS Y ARCHIVO (LOCAL / WEB / QUITAR) -->
          <div v-if="tabActiva === 'info'" class="tab-content-info">
            <div class="form-group">
              <label class="form-label-3d">Nombre del documento</label>
              <div class="input-3d-wrapper">
                <span class="input-3d-icon">📄</span>
                <input type="text" class="form-input-3d" v-model="docEdicion.nombre" placeholder="Nombre oficial del documento" />
              </div>
            </div>

            <div class="form-grid">
              <div class="form-group">
                <label class="form-label-3d">Tipo de documento</label>
                <select class="form-input-3d select-3d" v-model="docEdicion.tipo">
                  <option value="Certificado">Certificado</option>
                  <option value="Identidad">Identidad</option>
                  <option value="Diploma">Diploma</option>
                  <option value="Contrato">Contrato</option>
                  <option value="Factura">Factura</option>
                </select>
              </div>

              <div class="form-group">
                <label class="form-label-3d">Estado de verificación</label>
                <select class="form-input-3d select-3d" v-model="docEdicion.estado">
                  <option value="Guardado">Guardado</option>
                  <option value="Pendiente">Pendiente</option>
                  <option value="Aprobado">Aprobado</option>
                </select>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label-3d">Fecha de emisión registrada</label>
              <input type="text" class="form-input-3d" v-model="docEdicion.fecha" />
            </div>

            <!-- SECCIÓN 3D DE ARCHIVO ADJUNTO (SUBIR LOCAL / WEB / QUITAR) -->
            <div class="attachment-section-3d">
              <div class="attachment-header-3d">
                <span class="attachment-title-3d">Archivo digital en bóveda</span>
                <span class="attachment-sub-3d">Respaldo seguro cifrado</span>
              </div>

              <!-- Si ya tiene un archivo adjunto: Tarjeta 3D Elevada -->
              <div v-if="docEdicion.archivo" class="file-card-3d">
                <div class="file-card-3d-badge">
                  <span class="file-card-3d-ext">{{ (docEdicion.archivo.nombre || '').split('.').pop()?.toUpperCase() || 'DOC' }}</span>
                </div>
                <div class="file-card-3d-info">
                  <span class="file-card-3d-name">{{ docEdicion.archivo.nombre }}</span>
                  <div class="file-card-3d-meta">
                    <span class="file-card-3d-tag">
                      {{ docEdicion.archivo.origen === 'local' ? '📁 Origen Local' : '🌐 Enlace Web' }}
                    </span>
                    <span class="file-card-3d-check">✓ Archivo Vinculado</span>
                  </div>
                </div>
                <!-- BOTÓN 3D QUITAR DOCUMENTO -->
                <button class="btn-3d-remove" @click="quitarArchivo" title="Quitar archivo adjunto">
                  <svg class="w-4 h-4 mr-1.5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
                  </svg>
                  <span>Quitar archivo</span>
                </button>
              </div>

              <!-- Si NO tiene archivo adjunto: Opciones 3D de subida -->
              <div v-else class="upload-options-container">
                <div class="upload-tabs-selector">
                  <button
                    :class="['upload-tab-btn', origenSubida === 'local' ? 'active-upload-tab' : '']"
                    @click="origenSubida = 'local'"
                  >
                    📁 Subir desde Local
                  </button>
                  <button
                    :class="['upload-tab-btn', origenSubida === 'web' ? 'active-upload-tab' : '']"
                    @click="origenSubida = 'web'"
                  >
                    🌐 Vincular desde Web (URL)
                  </button>
                </div>

                <!-- Subir archivo Local -->
                <div v-if="origenSubida === 'local'" class="local-upload-dropzone">
                  <input type="file" id="localFileInput" class="hidden-file-input" @change="manejarArchivoLocal" />
                  <label for="localFileInput" class="dropzone-label">
                    <span class="dropzone-icon">📥</span>
                    <span class="dropzone-text">Seleccionar archivo desde este dispositivo</span>
                    <span class="dropzone-sub">Compatible con PDF, DOCX, XLSX, PNG, JPG</span>
                  </label>
                </div>

                <!-- Subir desde Web (URL) -->
                <div v-if="origenSubida === 'web'" class="web-url-upload-box">
                  <input
                    type="url"
                    class="form-input"
                    placeholder="https://ejemplo.com/documentos/mi-certificado.pdf"
                    v-model="urlArchivoWeb"
                  />
                  <button class="btn-attach-web" @click="vincularArchivoWeb">
                    <span>Adjuntar URL</span>
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- PESTAÑA 2: VISUALIZADOR Y EDITOR DE TEXTO ESTILO WORD CON RELIEVE 3D -->
          <div v-if="tabActiva === 'word'" class="tab-content-word">
            <!-- Barra de herramientas estilo Microsoft Word en relieve 3D -->
            <div class="word-ribbon-toolbar-3d">
              <div class="toolbar-group">
                <button class="ribbon-btn-3d" @click="aplicarFormato('bold')" title="Negrita"><strong>B</strong></button>
                <button class="ribbon-btn-3d" @click="aplicarFormato('italic')" title="Cursiva"><em>I</em></button>
                <button class="ribbon-btn-3d" @click="aplicarFormato('underline')" title="Subrayado"><u>U</u></button>
              </div>
              <div class="toolbar-divider-3d"></div>
              <div class="toolbar-group">
                <button class="ribbon-btn-3d" @click="agregarEncabezado" title="Título de documento">H1</button>
                <button class="ribbon-btn-3d" @click="agregarVineta" title="Lista de viñetas">• Lista</button>
              </div>
              <div class="toolbar-divider-3d"></div>
              <div class="toolbar-group">
                <button class="ribbon-btn-3d btn-clear-3d" @click="docEdicion.texto = ''" title="Borrar todo el texto">
                  🧹 Borrar texto
                </button>
              </div>
              <div class="toolbar-status-badge-3d">
                <span>✓ Edición Word Activa</span>
              </div>
            </div>

            <!-- Lienzo de Hoja de Papel estilo Documento Word con sombra 3D -->
            <div class="word-canvas-wrapper-3d">
              <!-- Regla superior simulada -->
              <div class="word-ruler">
                <span>|...|...|...|...|...|...|...|...|...|...|...|...|...|...|</span>
              </div>

              <!-- Hoja de papel A4/Carta blanca con elevación y textura de papel -->
              <div class="word-paper-sheet-3d">
                <textarea
                  class="word-paper-textarea-3d"
                  v-model="docEdicion.texto"
                  placeholder="Redacta, visualiza o borra aquí el texto de tu documento como en Microsoft Word..."
                ></textarea>
              </div>

              <!-- Barra de estado inferior de Word -->
              <div class="word-status-footer-3d">
                <span>Página 1 de 1</span>
                <span>{{ contarPalabras(docEdicion.texto) }} palabras</span>
                <span>{{ docEdicion.texto ? docEdicion.texto.length : 0 }} caracteres</span>
                <span class="word-badge-lang">Español (Colombia)</span>
              </div>
            </div>
          </div>
        </div>

        <div class="modal-footer modal-3d-footer">
          <button class="btn-3d-secondary" @click="mostrarModalEditar = false">Cancelar</button>
          <button class="btn-3d-primary" @click="guardarEdicion">
            <svg class="w-4 h-4 mr-1.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
            </svg>
            <span>Guardar Cambios</span>
          </button>
        </div>
      </div>
    </div>

    <!-- MODAL PROFESIONAL: ADJUNTAR NUEVO DOCUMENTO (LOCAL Y WEB) -->
    <div v-if="mostrarModalNuevo" class="modal-backdrop" @click.self="mostrarModalNuevo = false">
      <div class="modal-card modal-pro-card">
        <!-- Encabezado Limpio sin icono verde ni texto descriptivo -->
        <div class="modal-header modal-pro-header">
          <h3 class="modal-pro-title-clean">Adjuntar Nuevo Documento</h3>
          <button class="modal-close-btn-pro" @click="mostrarModalNuevo = false" title="Cerrar ventana">✕</button>
        </div>

        <div class="modal-body modal-pro-body">
          <!-- DATOS PRINCIPALES -->
          <div class="form-group">
            <label class="form-label">
              <span>Nombre del documento</span>
              <span class="label-required">*</span>
            </label>
            <div class="input-with-icon">
              <span class="input-icon">📄</span>
              <input
                type="text"
                class="form-input input-padded"
                placeholder="Ej. Certificado Bancario Davivienda 2026"
                v-model="nuevoDoc.nombre"
              />
            </div>
          </div>

          <div class="form-grid">
            <div class="form-group">
              <label class="form-label">Tipo de documento</label>
              <select class="form-input" v-model="nuevoDoc.tipo">
                <option value="Certificado">Certificado</option>
                <option value="Identidad">Identidad</option>
                <option value="Diploma">Diploma</option>
                <option value="Contrato">Contrato</option>
                <option value="Factura">Factura / Recibo</option>
              </select>
            </div>

            <div class="form-group">
              <label class="form-label">Estado inicial</label>
              <select class="form-input" v-model="nuevoDoc.estado">
                <option value="Guardado">Guardado</option>
                <option value="Pendiente">Pendiente</option>
                <option value="Aprobado">Aprobado</option>
              </select>
            </div>
          </div>

          <div class="form-group">
            <label class="form-label">Fecha de registro o expedición</label>
            <input type="text" class="form-input" v-model="nuevoDoc.fecha" placeholder="DD/MM/AAAA" />
          </div>

          <!-- SECCIÓN PROFESIONAL: SUBIDA LOCAL Y WEB -->
          <div class="upload-pro-box">
            <div class="upload-pro-header">
              <span class="upload-pro-title">Archivo Digital Adjunto</span>
              <span class="upload-pro-sub">Elige el método de incorporación</span>
            </div>

            <!-- Selector de Método: Local vs Web -->
            <div class="upload-method-selector">
              <button
                type="button"
                :class="['upload-method-tab', origenNuevoSubida === 'local' ? 'active-method' : '']"
                @click="origenNuevoSubida = 'local'"
              >
                <svg class="w-4 h-4 mr-1.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 7v10a2 2 0 002 2h14a2 2 0 002-2V9a2 2 0 00-2-2h-6l-2-2H5a2 2 0 00-2 2z" />
                </svg>
                <span>Subir desde Local</span>
              </button>
              <button
                type="button"
                :class="['upload-method-tab', origenNuevoSubida === 'web' ? 'active-method' : '']"
                @click="origenNuevoSubida = 'web'"
              >
                <svg class="w-4 h-4 mr-1.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9c1.657 0 3-4.03 3-9s-1.343-9-3-9m0 18c-1.657 0-3-4.03-3-9s1.343-9 3-9m-9 9a9 9 0 019-9" />
                </svg>
                <span>Vincular desde Web (URL)</span>
              </button>
            </div>

            <!-- CASO 1: Archivo seleccionado actualmente (ya sea local o web) -->
            <div v-if="nuevoDocArchivo" class="attached-file-preview-card">
              <div class="file-preview-badge">
                <span class="file-preview-ext">{{ nuevoDocArchivo.tipo || 'DOC' }}</span>
              </div>
              <div class="file-preview-details">
                <span class="file-preview-name">{{ nuevoDocArchivo.nombre }}</span>
                <div class="file-preview-meta">
                  <span class="file-preview-tag">{{ nuevoDocArchivo.origen === 'local' ? '📁 Archivo Local' : '🌐 Enlace Web' }}</span>
                  <span v-if="nuevoDocArchivo.size" class="file-preview-size">• {{ nuevoDocArchivo.size }}</span>
                  <span class="file-ready-tag">✓ Listo para guardar</span>
                </div>
              </div>
              <button type="button" class="btn-change-file" @click="quitarArchivoNuevo" title="Cambiar archivo">
                ✕ Cambiar
              </button>
            </div>

            <!-- CASO 2: Sin archivo - MODO LOCAL -->
            <div v-else-if="origenNuevoSubida === 'local'" class="local-dropzone-pro">
              <input
                type="file"
                id="nuevoDocFileInput"
                class="hidden-file-input"
                @change="manejarArchivoNuevoLocal"
                accept=".pdf,.doc,.docx,.xls,.xlsx,.png,.jpg,.jpeg"
              />
              <label for="nuevoDocFileInput" class="dropzone-label-pro">
                <div class="dropzone-icon-circle">
                  <svg class="w-7 h-7 text-emerald-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" />
                  </svg>
                </div>
                <div class="dropzone-text-group">
                  <span class="dropzone-hint">Formatos soportados: <strong>PDF, DOCX, XLSX, JPG, PNG</strong> (Hasta 25 MB)</span>
                </div>
              </label>
            </div>

            <!-- CASO 3: Sin archivo - MODO WEB URL -->
            <div v-else-if="origenNuevoSubida === 'web'" class="web-url-pro-box">
              <div class="web-input-group">
                <span class="web-input-icon">🔗</span>
                <input
                  type="url"
                  class="form-input web-input-field"
                  placeholder="https://ejemplo.com/documentos/mi-certificado.pdf"
                  v-model="urlNuevoWeb"
                  @keyup.enter="vincularWebNuevo"
                />
                <button type="button" class="btn-link-web" @click="vincularWebNuevo" :disabled="!urlNuevoWeb.trim()">
                  Vincular
                </button>
              </div>
              <p class="web-helper-text">
                Ingresa el enlace público o privado al archivo. El sistema guardará la referencia segura con acceso directo.
              </p>
            </div>
          </div>

          <!-- REDACTAR CONTENIDO O NOTAS (OPCIONAL) -->
          <div class="form-group">
            <div class="label-with-counter">
              <label class="form-label">Redactar contenido de texto o notas (Opcional)</label>
              <span class="text-counter">{{ contarPalabras(nuevoDoc.texto) }} palabras</span>
            </div>
            <textarea
              class="form-input form-textarea-modern"
              placeholder="Escribe anotaciones, transcripción o el contenido relevante de este documento..."
              v-model="nuevoDoc.texto"
            ></textarea>
          </div>
        </div>

        <div class="modal-footer modal-pro-footer">
          <button type="button" class="btn-secondary" @click="mostrarModalNuevo = false">Cancelar</button>
          <button type="button" class="btn-primary-action" @click="agregarDocumento">
            <svg class="w-4 h-4 mr-1.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
            </svg>
            <span>Subir y Guardar Documento</span>
          </button>
        </div>
      </div>
    </div>

  </div>
</template>

<script setup lang="ts">
import { ref, computed, watch } from 'vue';

const guardados = ref(5);
const pendientes = ref(1);
const enviados = ref(4);
const eliminados = ref(0);
const colaboradores = ref(2);

// Filtros reactivos
const busqueda = ref('');
const estadoFiltro = ref('');
const tipoFiltro = ref('');

const totalDocs = computed(() => guardados.value + pendientes.value + enviados.value);

// Altura de barras proporcional y segura
function getBarHeight(val: number) {
  const max = Math.max(guardados.value, pendientes.value, enviados.value, colaboradores.value, 1);
  const px = Math.round(22 + (val / max) * 36);
  return `${px}px`;
}

interface ArchivoDoc {
  origen: string;
  nombre: string;
  url?: string;
  size?: string;
  tipo?: string;
}

interface DocumentoItem {
  id: number;
  nombre: string;
  tipo: string;
  fecha: string;
  estado: string;
  archivo: ArchivoDoc;
  texto: string;
}

// Lista de documentos reactiva con archivos y textos editables
const documentos = ref<DocumentoItem[]>([
  {
    id: 1,
    nombre: 'Certificado EPS',
    tipo: 'Certificado',
    fecha: '20/10/2025',
    estado: 'Guardado',
    archivo: { origen: 'local', nombre: 'Certificado_EPS_2025.pdf', url: '' },
    texto: `CERTIFICADO DE AFILIACIÓN EN SALUD

Por medio de la presente, la entidad prestadora de salud certifica que el titular se encuentra debidamente afiliado en calidad de Cotizante Principal con estado ACTIVO y al día con sus aportes correspondientes.

Vigencia: Octubre 2025 - Octubre 2026.
Emitido en Bogotá D.C.`
  },
  {
    id: 2,
    nombre: 'Cedula',
    tipo: 'Identidad',
    fecha: '18/10/2025',
    estado: 'Pendiente',
    archivo: { origen: 'web', nombre: 'cedula_identidad_escaneada.png', url: 'https://vault.archiment.internal/docs/cedula_1020.png' },
    texto: `REPÚBLICA DE COLOMBIA
DOCUMENTO NACIONAL DE IDENTIDAD

Número de Identificación: 1.020.304.050
Apellidos y Nombres: CIUDADANO TITULAR
Fecha de Nacimiento: 15/05/1998
Lugar de Expedición: Bogotá D.C.
Estatura: 1.75 m • Grupo Sanguíneo: O+`
  },
  {
    id: 3,
    nombre: 'Diploma Universidad',
    tipo: 'Certificado',
    fecha: '15/10/2025',
    estado: 'Aprobado',
    archivo: { origen: 'local', nombre: 'Diploma_Grado_Universitario.pdf', url: '' },
    texto: `REPÚBLICA Y CONSEJO ACADÉMICO SUPERIOR
DIPLOMA DE GRADO PROFESIONAL

Hace constar que el estudiante ha cursado y aprobado con honores todos los créditos y requisitos académicos correspondientes, confiriéndole el título profesional de:

INGENIERO DE SISTEMAS Y CIENCIAS DE LA COMPUTACIÓN

Registrado en acta de grado No. 481-2025.`
  },
  {
    id: 4,
    nombre: 'Contrato Laboral Indefinido',
    tipo: 'Contrato',
    fecha: '02/09/2025',
    estado: 'Guardado',
    archivo: { origen: 'local', nombre: 'Contrato_Laboral_2025.pdf', url: '' },
    texto: `CONTRATO INDIVIDUAL DE TRABAJO A TÉRMINO INDEFINIDO

Entre el empleador y el trabajador se celebra el presente contrato bajo las estipulaciones de ley vigentes, desempeñando el cargo de Líder de Desarrollo de Software.`
  },
  {
    id: 5,
    nombre: 'Certificado Bancario Davivienda',
    tipo: 'Certificado',
    fecha: '28/08/2025',
    estado: 'Aprobado',
    archivo: { origen: 'web', nombre: 'Certificado_Cuenta_Ahorros.pdf', url: 'https://davivienda.internal/docs/cert_cuenta.pdf' },
    texto: `BANCO DAVIVIENDA S.A.
CERTIFICACIÓN DE CUENTA BANCARIA

Certificamos que el titular mantiene con nuestra institución una Cuenta de Ahorros activa y con excelente manejo comercial.`
  },
  {
    id: 6,
    nombre: 'RUT DIAN Actualizado',
    tipo: 'Certificado',
    fecha: '14/08/2025',
    estado: 'Guardado',
    archivo: { origen: 'local', nombre: 'RUT_DIAN_2025.pdf', url: '' },
    texto: `REGISTRO ÚNICO TRIBUTARIO - DIAN
Identificación tributaria vigente para el año fiscal 2025-2026. Actividad principal: 6201 Desarrollo de sistemas informáticos.`
  },
  {
    id: 7,
    nombre: 'Pasaporte Vigente',
    tipo: 'Identidad',
    fecha: '10/06/2025',
    estado: 'Guardado',
    archivo: { origen: 'local', nombre: 'Pasaporte_Biometrico.pdf', url: '' },
    texto: `REPÚBLICA DE COLOMBIA - MINISTERIO DE RELACIONES EXTERIORES
PASAPORTE ORDINARIO ELECTRÓNICO
Válido para viajar a todos los países del mundo.`
  }
]);

// Filtro en tiempo real
const documentosFiltrados = computed(() => {
  return documentos.value.filter((doc) => {
    const matchBusqueda =
      !busqueda.value ||
      doc.nombre.toLowerCase().includes(busqueda.value.toLowerCase()) ||
      doc.tipo.toLowerCase().includes(busqueda.value.toLowerCase()) ||
      doc.fecha.includes(busqueda.value);

    const matchEstado = !estadoFiltro.value || doc.estado === estadoFiltro.value;
    const matchTipo = !tipoFiltro.value || doc.tipo === tipoFiltro.value;

    return matchBusqueda && matchEstado && matchTipo;
  });
});

// PAGINACIÓN REACTIVA
const paginaActual = ref(1);
const itemsPorPagina = ref(5);

const totalPaginas = computed(() => {
  const total = Math.ceil(documentosFiltrados.value.length / itemsPorPagina.value);
  return total > 0 ? total : 1;
});

const indiceInicio = computed(() => (paginaActual.value - 1) * itemsPorPagina.value);
const indiceFin = computed(() => indiceInicio.value + itemsPorPagina.value);

const documentosPaginados = computed(() => {
  return documentosFiltrados.value.slice(indiceInicio.value, indiceFin.value);
});

function irAPagina(pag: number) {
  if (pag >= 1 && pag <= totalPaginas.value) {
    paginaActual.value = pag;
  }
}

function cambiarItemsPorPagina() {
  paginaActual.value = 1;
}

watch([busqueda, estadoFiltro, tipoFiltro], () => {
  paginaActual.value = 1;
});

// Clase de color según estado
function getStatusClass(estado: string) {
  if (estado === 'Guardado') return 'status-guardado';
  if (estado === 'Pendiente') return 'status-pendiente';
  if (estado === 'Aprobado') return 'status-aprobado';
  return '';
}

// CONTROL DE VISUALIZACIÓN EN TAMAÑO A4 COMPLETO
const mostrarModalVisualizar = ref(false);
const docVisualizando = ref<any>(null);

function abrirVisualizar(doc: any) {
  docVisualizando.value = doc;
  mostrarModalVisualizar.value = true;
}

function imprimirDocumento() {
  window.print();
}

// CONTROL DE EDICIÓN Y GESTIÓN DE ARCHIVOS / EDITOR WORD
const mostrarModalEditar = ref(false);
const docIndexEditando = ref(-1);
const tabActiva = ref<'info' | 'word'>('info');
const origenSubida = ref<'local' | 'web'>('local');
const urlArchivoWeb = ref('');

const docEdicion = ref({
  id: 0,
  nombre: '',
  tipo: 'Certificado',
  fecha: '',
  estado: 'Guardado',
  archivo: null as any,
  texto: '',
});

function abrirEditar(doc: any) {
  docIndexEditando.value = documentos.value.findIndex(d => d.id === doc.id);
  docEdicion.value = JSON.parse(JSON.stringify(doc));
  tabActiva.value = 'info';
  origenSubida.value = 'local';
  urlArchivoWeb.value = '';
  mostrarModalEditar.value = true;
}

// Quitar archivo adjunto
function quitarArchivo() {
  docEdicion.value.archivo = null;
}

// Cargar archivo local
function manejarArchivoLocal(e: Event) {
  const target = e.target as HTMLInputElement;
  if (target.files && target.files.length > 0 && target.files[0]) {
    const file = target.files[0];
    docEdicion.value.archivo = {
      origen: 'local',
      nombre: file.name,
      url: '',
    };
  }
}

// Vincular archivo web
function vincularArchivoWeb() {
  if (!urlArchivoWeb.value.trim()) return;
  const url = urlArchivoWeb.value.trim();
  const nombre = url.split('/').pop() || 'documento_web.pdf';
  docEdicion.value.archivo = {
    origen: 'web',
    nombre: nombre,
    url: url,
  };
  urlArchivoWeb.value = '';
}

// Guardar cambios de edición
function guardarEdicion() {
  if (docIndexEditando.value >= 0 && docIndexEditando.value < documentos.value.length) {
    documentos.value[docIndexEditando.value] = { ...docEdicion.value };
  }
  mostrarModalEditar.value = false;
}

// Herramientas del editor de Word
function aplicarFormato(tipo: string) {
  if (!docEdicion.value.texto) return;
  if (tipo === 'bold') {
    docEdicion.value.texto += '\n**TEXTO EN NEGRITA**';
  } else if (tipo === 'italic') {
    docEdicion.value.texto += '\n*Texto en cursiva*';
  } else if (tipo === 'underline') {
    docEdicion.value.texto += '\n__Texto subrayado__';
  }
}

function agregarEncabezado() {
  docEdicion.value.texto = (docEdicion.value.texto ? docEdicion.value.texto + '\n\n' : '') + '# NUEVO ENCABEZADO OFICIAL';
}

function agregarVineta() {
  docEdicion.value.texto = (docEdicion.value.texto ? docEdicion.value.texto + '\n' : '') + '• Punto de documento';
}

function contarPalabras(texto: string) {
  if (!texto) return 0;
  return texto.trim().split(/\s+/).filter(Boolean).length;
}

// Control de Eliminación
function eliminarDoc(doc: any) {
  const index = documentos.value.findIndex(d => d.id === doc.id);
  if (index === -1) return;
  if (confirm(`¿Estás seguro de eliminar "${doc.nombre}"?`)) {
    documentos.value.splice(index, 1);
    eliminados.value++;
    if (guardados.value > 0 && doc.estado === 'Guardado') guardados.value--;
    if (pendientes.value > 0 && doc.estado === 'Pendiente') pendientes.value--;
    if (paginaActual.value > totalPaginas.value) {
      paginaActual.value = Math.max(1, totalPaginas.value);
    }
  }
}

// Control de Nuevo Documento Profesional (Local y Web)
const mostrarModalNuevo = ref(false);
const origenNuevoSubida = ref<'local' | 'web'>('local');
const urlNuevoWeb = ref('');
const nuevoDocArchivo = ref<{
  nombre: string;
  size?: string;
  tipo?: string;
  origen: 'local' | 'web';
  url?: string;
} | null>(null);

const nuevoDoc = ref({
  nombre: '',
  tipo: 'Certificado',
  fecha: new Date().toLocaleDateString('es-CO'),
  estado: 'Guardado',
  texto: '',
});

function abrirModalNuevo() {
  nuevoDoc.value = {
    nombre: '',
    tipo: 'Certificado',
    fecha: new Date().toLocaleDateString('es-CO'),
    estado: 'Guardado',
    texto: '',
  };
  nuevoDocArchivo.value = null;
  urlNuevoWeb.value = '';
  origenNuevoSubida.value = 'local';
  mostrarModalNuevo.value = true;
}

function manejarArchivoNuevoLocal(e: Event) {
  const target = e.target as HTMLInputElement;
  if (target.files && target.files.length > 0 && target.files[0]) {
    const file = target.files[0];
    const sizeFormatted = file.size > 1024 * 1024
      ? (file.size / (1024 * 1024)).toFixed(2) + ' MB'
      : (file.size / 1024).toFixed(1) + ' KB';
    
    nuevoDocArchivo.value = {
      nombre: file.name,
      size: sizeFormatted,
      origen: 'local',
      tipo: file.name.split('.').pop()?.toUpperCase() || 'DOC'
    };

    if (!nuevoDoc.value.nombre.trim()) {
      nuevoDoc.value.nombre = file.name.replace(/\.[^/.]+$/, '').replace(/[-_]/g, ' ');
    }
  }
}

function vincularWebNuevo() {
  if (!urlNuevoWeb.value.trim()) return;
  const url = urlNuevoWeb.value.trim();
  const nombre = url.split('/').pop()?.split('?')[0] || 'documento_web.pdf';
  nuevoDocArchivo.value = {
    nombre: nombre,
    size: 'Enlace Web',
    origen: 'web',
    url: url,
    tipo: nombre.split('.').pop()?.toUpperCase() || 'URL'
  };
  if (!nuevoDoc.value.nombre.trim()) {
    nuevoDoc.value.nombre = nombre.replace(/\.[^/.]+$/, '').replace(/[-_]/g, ' ');
  }
}

function quitarArchivoNuevo() {
  nuevoDocArchivo.value = null;
  urlNuevoWeb.value = '';
}

function agregarDocumento() {
  if (!nuevoDoc.value.nombre.trim()) {
    alert('Por favor ingresa un nombre para el documento.');
    return;
  }

  let archivoFinal = nuevoDocArchivo.value;
  if (!archivoFinal) {
    if (origenNuevoSubida.value === 'web' && urlNuevoWeb.value.trim()) {
      const url = urlNuevoWeb.value.trim();
      const nombre = url.split('/').pop()?.split('?')[0] || 'documento_web.pdf';
      archivoFinal = {
        nombre: nombre,
        size: 'Enlace Web',
        origen: 'web',
        url: url,
        tipo: nombre.split('.').pop()?.toUpperCase() || 'URL'
      };
    } else {
      archivoFinal = {
        nombre: nuevoDoc.value.nombre.replace(/\s+/g, '_') + '.pdf',
        size: '1.4 MB',
        origen: 'local',
        url: '',
        tipo: 'PDF'
      };
    }
  }

  documentos.value.unshift({
    id: Date.now(),
    nombre: nuevoDoc.value.nombre,
    tipo: nuevoDoc.value.tipo,
    fecha: nuevoDoc.value.fecha || new Date().toLocaleDateString('es-CO'),
    estado: nuevoDoc.value.estado,
    archivo: archivoFinal,
    texto: nuevoDoc.value.texto || 'Contenido oficial del documento registrado en bóveda.',
  });

  guardados.value++;
  mostrarModalNuevo.value = false;
}
</script>

<style scoped>
/* CONTENEDOR PEGADO A LA IZQUIERDA Y ELEVADO */
.container {
  padding: 16px 32px 48px 24px;
  max-width: 100%;
  margin: 0;
  box-sizing: border-box;
}

.title-main {
  color: #16a34a;
  font-size: 28px;
  font-weight: 700;
  margin: 0 0 24px 0;
  line-height: 1.25;
}

/* LAYOUT EN DOS COLUMNAS: SIDEBAR ANCLADA A LA IZQUIERDA */
.dashboard-layout {
  display: flex;
  gap: 32px;
  align-items: flex-start;
  width: 100%;
}

/* COLUMNA IZQUIERDA (PANEL 3D PEGADO A LA IZQUIERDA) */
.stats-sidebar {
  width: 350px;
  flex-shrink: 0;
}

.stats-card {
  background: white;
  border: 1px solid #e2e8f0;
  border-radius: 16px;
  padding: 24px;
  box-shadow: 0 10px 25px -5px rgba(10, 42, 94, 0.08), 0 8px 10px -6px rgba(10, 42, 94, 0.04);
}

.stats-card-header {
  margin-bottom: 16px;
}

.stats-card-title {
  font-size: 17px;
  font-weight: 800;
  color: #0A2A5E;
  margin: 0;
}

.stats-card-subtitle {
  font-size: 11px;
  font-weight: 600;
  color: #64748b;
  margin: 2px 0 0 0;
}

/* GRÁFICO 3D DONUT */
.chart-3d-wrapper {
  background: linear-gradient(180deg, #f8fafc 0%, #f1f5f9 100%);
  border: 1px solid #e2e8f0;
  border-radius: 14px;
  padding: 16px;
  margin-bottom: 20px;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.03);
}

.chart-3d-scene {
  position: relative;
  width: 140px;
  height: 140px;
  margin: 0 auto;
  perspective: 500px;
}

.donut-3d-svg {
  width: 100%;
  height: 100%;
  transform: rotateX(25deg);
  transform-style: preserve-3d;
  filter: drop-shadow(0 6px 8px rgba(10, 42, 94, 0.18));
}

.chart-center-hub {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.hub-count {
  font-size: 22px;
  font-weight: 900;
  color: #0A2A5E;
  line-height: 1;
}

.hub-label {
  font-size: 10px;
  font-weight: 700;
  color: #64748b;
  text-transform: uppercase;
  margin-top: 2px;
}

.chart-legend-3d {
  display: flex;
  justify-content: center;
  gap: 8px;
  margin-top: 12px;
  flex-wrap: wrap;
}

.leg-pill {
  font-size: 11px;
  font-weight: 700;
  padding: 3px 8px;
  border-radius: 20px;
  display: inline-flex;
  align-items: center;
  gap: 4px;
}

.dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
}

.pill-green { background: #dcfce7; color: #15803d; }
.pill-green .dot { background: #15803d; }

.pill-blue { background: #dbeafe; color: #1d4ed8; }
.pill-blue .dot { background: #1d4ed8; }

.pill-amber { background: #fef3c7; color: #b45309; }
.pill-amber .dot { background: #b45309; }

/* BARRAS ISOMÉTRICAS 3D CON ESPACIADO GENEROSO */
.bar-chart-3d-box {
  background: white;
  border: 1px solid #e2e8f0;
  border-radius: 14px;
  padding: 16px 16px 14px 16px;
  margin-bottom: 20px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.03);
}

.bar-chart-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 24px;
}

.bar-chart-title {
  font-size: 11px;
  font-weight: 800;
  color: #475569;
  text-transform: uppercase;
  letter-spacing: 0.8px;
  margin: 0;
}

.bar-chart-tag {
  font-size: 9px;
  font-weight: 800;
  background: #f1f5f9;
  color: #64748b;
  padding: 2px 6px;
  border-radius: 6px;
  text-transform: uppercase;
}

.bars-isometric-container {
  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  height: 90px;
  padding-bottom: 4px;
  border-bottom: 2px solid #f1f5f9;
}

.iso-bar-col {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
  width: 44px;
}

.iso-bar {
  position: relative;
  width: 26px;
  border-radius: 4px 4px 0 0;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  padding-top: 4px;
  transition: height 0.3s ease;
  box-shadow: 2px 4px 8px rgba(0, 0, 0, 0.15);
}

.iso-val {
  font-size: 10px;
  font-weight: 900;
  color: white;
}

.iso-lbl {
  font-size: 10px;
  font-weight: 700;
  color: #64748b;
}

.bar-green { background: linear-gradient(180deg, #22c55e 0%, #15803d 100%); }
.bar-amber { background: linear-gradient(180deg, #f59e0b 0%, #b45309 100%); }
.bar-blue  { background: linear-gradient(180deg, #3b82f6 0%, #1d4ed8 100%); }
.bar-purple{ background: linear-gradient(180deg, #a855f7 0%, #7e22ce 100%); }

/* LISTA DE MÉTRICAS */
.stats-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.hidden-defs {
  position: absolute;
  width: 0;
  height: 0;
  pointer-events: none;
}

.stat-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 12px;
  border-radius: 10px;
  background-color: #f8fafc;
  border: 1px solid #f1f5f9;
  transition: all 0.2s ease;
}

.stat-item:hover {
  background-color: #ffffff;
  border-color: #cbd5e1;
  transform: translateX(3px);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
}

.stat-left {
  display: flex;
  align-items: center;
  gap: 12px;
  flex: 1;
}

.stat-icon-3d {
  width: 34px;
  height: 34px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: white;
  box-shadow: 0 2px 6px rgba(0,0,0,0.08);
  border: 1px solid #e2e8f0;
  flex-shrink: 0;
}

.realistic-svg {
  width: 20px;
  height: 20px;
}

.stat-label {
  font-size: 12px;
  font-weight: 700;
  color: #334155;
  display: block;
}

.stat-progress-bg {
  width: 130px;
  height: 4px;
  background: #e2e8f0;
  border-radius: 9999px;
  margin-top: 4px;
  overflow: hidden;
}

.stat-progress-fill {
  height: 100%;
  border-radius: 9999px;
  transition: width 0.4s ease;
}

.fill-green { background: #22c55e; }
.fill-amber { background: #f59e0b; }
.fill-blue  { background: #3b82f6; }
.fill-red   { background: #ef4444; }
.fill-purple{ background: #a855f7; }

.stat-number {
  font-size: 15px;
  font-weight: 900;
  padding: 2px 8px;
  border-radius: 8px;
  min-width: 24px;
  text-align: center;
}

.num-green  { background: #dcfce7; color: #15803d; }
.num-amber  { background: #fef3c7; color: #b45309; }
.num-blue   { background: #dbeafe; color: #1d4ed8; }
.num-red    { background: #fee2e2; color: #b91c1c; }
.num-purple { background: #f3e8ff; color: #7e22ce; }

.divider {
  border: none;
  border-top: 1px solid #e2e8f0;
  margin: 18px 0;
}

.secure-line {
  display: flex;
  align-items: center;
  gap: 8px;
}

.shield {
  position: relative;
  font-size: 18px;
}

.check {
  color: #16a34a;
  font-size: 12px;
  position: absolute;
  bottom: -2px;
  right: -4px;
  background: white;
  border-radius: 50%;
}

.secure-text {
  font-size: 11px;
  color: #64748b;
  line-height: 1.4;
  font-weight: 600;
}

/* COLUMNA DERECHA: ESTILO ENTERPRISE */
.main-content {
  flex: 1;
  min-width: 0;
}

.content-header-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 20px;
}

.organiza-title {
  font-size: 21px;
  font-weight: 800;
  color: #0A2A5E;
  margin: 0;
  letter-spacing: -0.3px;
}

.organiza-subtitle {
  font-size: 13px;
  color: #64748b;
  margin: 4px 0 0 0;
  font-weight: 500;
}

.btn-green-action {
  background: linear-gradient(135deg, #16a34a 0%, #15803d 100%);
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 10px;
  font-weight: 700;
  font-size: 14px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 6px;
  box-shadow: 0 4px 12px rgba(22, 163, 74, 0.3);
  transition: all 0.2s ease;
  white-space: nowrap;
}

.btn-green-action:hover {
  transform: translateY(-1px);
  box-shadow: 0 6px 16px rgba(22, 163, 74, 0.4);
}

/* PANEL DE CONTROL: BUSCADOR Y FILTROS */
.control-panel-card {
  background: white;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  padding: 14px 18px;
  margin-bottom: 18px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.02);
}

.search-box-pro {
  position: relative;
  display: flex;
  align-items: center;
  width: 100%;
}

.search-icon-svg {
  position: absolute;
  left: 14px;
  width: 18px;
  height: 18px;
  color: #94a3b8;
  pointer-events: none;
}

.search-input-pro {
  width: 100%;
  padding: 10px 38px 10px 42px;
  border: 1.5px solid #e2e8f0;
  border-radius: 10px;
  font-size: 14px;
  color: #1e293b;
  background-color: #f8fafc;
  outline: none;
  transition: all 0.2s ease;
}

.search-input-pro:focus {
  background-color: #ffffff;
  border-color: #16a34a;
  box-shadow: 0 0 0 3px rgba(22, 163, 74, 0.15);
}

.clear-search-btn {
  position: absolute;
  right: 12px;
  background: #e2e8f0;
  border: none;
  color: #64748b;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  font-size: 11px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* GRUPO DE FILTROS */
.filter-controls-pro {
  display: flex;
  align-items: center;
  gap: 12px;
  flex-wrap: wrap;
}

.filter-label-group {
  display: flex;
  align-items: center;
  gap: 6px;
  color: #475569;
}

.filter-icon-svg {
  width: 16px;
  height: 16px;
  color: #64748b;
}

.filter-title {
  font-size: 13px;
  font-weight: 700;
  color: #334155;
}

.select-wrapper {
  position: relative;
}

.dropdown-pro {
  border: 1.5px solid #e2e8f0;
  border-radius: 8px;
  padding: 7px 14px;
  font-size: 13px;
  font-weight: 600;
  color: #334155;
  background: white;
  cursor: pointer;
  outline: none;
  transition: all 0.2s ease;
}

.dropdown-pro:focus {
  border-color: #16a34a;
  box-shadow: 0 0 0 3px rgba(22, 163, 74, 0.12);
}

.results-badge {
  margin-left: auto;
  font-size: 12px;
  font-weight: 700;
  color: #64748b;
  background: #f1f5f9;
  padding: 4px 10px;
  border-radius: 20px;
}

/* TABLA PROFESIONAL */
.table-container-pro {
  background: white;
  border-radius: 14px;
  border: 1px solid #e2e8f0;
  overflow: hidden;
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.04);
}

.docs-table-pro {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
}

.docs-table-pro thead {
  background: #f8fafc;
  border-bottom: 1.5px solid #e2e8f0;
}

.docs-table-pro th {
  padding: 14px 18px;
  font-size: 11.5px;
  font-weight: 800;
  color: #64748b;
  text-transform: uppercase;
  letter-spacing: 0.6px;
}

.th-actions {
  text-align: right;
  padding-right: 24px;
}

.table-row-pro {
  border-bottom: 1px solid #f1f5f9;
  transition: background-color 0.15s ease;
}

.table-row-pro:hover {
  background-color: #f8fafc;
}

.docs-table-pro td {
  padding: 14px 18px;
  font-size: 13.5px;
  color: #334155;
}

.td-doc-name {
  font-weight: 700;
  color: #0f172a;
}

.doc-text-name {
  font-size: 14px;
  font-weight: 700;
  color: #0A2A5E;
}

.type-pill {
  font-size: 12px;
  font-weight: 700;
  color: #475569;
  background: #f1f5f9;
  padding: 3px 8px;
  border-radius: 6px;
  border: 1px solid #e2e8f0;
}

.td-date {
  font-size: 13px;
  color: #64748b;
  font-weight: 500;
}

/* BADGES DE ESTADO CON PUNTOS DE COLOR */
.status-badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 3px 10px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 700;
}

.status-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
}

.status-guardado {
  background-color: #dcfce7;
  color: #15803d;
  border: 1px solid #bbf7d0;
}
.status-guardado .status-dot { background-color: #16a34a; }

.status-pendiente {
  background-color: #fef3c7;
  color: #b45309;
  border: 1px solid #fde68a;
}
.status-pendiente .status-dot { background-color: #f59e0b; }

.status-aprobado {
  background-color: #dbeafe;
  color: #1d4ed8;
  border: 1px solid #bfdbfe;
}
.status-aprobado .status-dot { background-color: #2563eb; }

/* BOTONES PROFESIONALES DE ACCIONES */
.td-actions {
  text-align: right;
  padding-right: 20px;
}

.actions-group {
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

/* BOTONES PROFESIONALES DE ACCIONES (SOLO ICONOS) */
.btn-action-icon {
  width: 34px;
  height: 34px;
  border-radius: 8px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: 1px solid transparent;
  cursor: pointer;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
  padding: 0;
}

.btn-edit-icon {
  background-color: #eff6ff;
  color: #2563eb;
  border-color: #dbeafe;
}

.btn-edit-icon:hover {
  background-color: #2563eb;
  color: white;
  border-color: #2563eb;
  transform: translateY(-1px);
  box-shadow: 0 4px 10px rgba(37, 99, 235, 0.25);
}

.btn-delete-icon {
  background-color: #fef2f2;
  color: #dc2626;
  border-color: #fee2e2;
}

.btn-delete-icon:hover {
  background-color: #dc2626;
  color: white;
  border-color: #dc2626;
  transform: translateY(-1px);
  box-shadow: 0 4px 10px rgba(220, 38, 38, 0.25);
}

/* ========================================================
   ESTILOS DE PAGINACIÓN PROFESIONAL
   ======================================================== */
.pagination-container-pro {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 20px;
  background: #ffffff;
  border-top: 1px solid #e2e8f0;
  border-bottom-left-radius: 12px;
  border-bottom-right-radius: 12px;
  flex-wrap: wrap;
  gap: 12px;
}

.pagination-info {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 13px;
  color: #64748b;
  font-weight: 500;
}

.pagination-highlight {
  font-weight: 700;
  color: #0A2A5E;
}

.pagination-size-selector {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 13px;
  color: #64748b;
}

.size-label {
  font-weight: 600;
}

.select-per-page {
  padding: 5px 10px;
  border: 1.5px solid #cbd5e1;
  border-radius: 6px;
  background: #f8fafc;
  color: #0A2A5E;
  font-weight: 700;
  font-size: 12.5px;
  cursor: pointer;
  outline: none;
  transition: all 0.2s ease;
}

.select-per-page:focus {
  border-color: #2563eb;
  background: white;
}

.pagination-controls {
  display: flex;
  align-items: center;
  gap: 6px;
}

.page-numbers-group {
  display: flex;
  align-items: center;
  gap: 4px;
}

.btn-page-nav {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 6px 12px;
  background: #f8fafc;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  font-size: 12.5px;
  font-weight: 700;
  color: #334155;
  cursor: pointer;
  transition: all 0.15s ease;
}

.btn-page-nav:hover:not(:disabled) {
  background: #ffffff;
  border-color: #2563eb;
  color: #2563eb;
  box-shadow: 0 2px 4px rgba(37, 99, 235, 0.1);
  transform: translateY(-1px);
}

.btn-page-nav:disabled {
  opacity: 0.45;
  cursor: not-allowed;
  background: #f1f5f9;
}

.btn-page-number {
  min-width: 32px;
  height: 32px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  border: 1px solid #cbd5e1;
  background: #ffffff;
  color: #334155;
  font-size: 12.5px;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.15s ease;
}

.btn-page-number:hover {
  background: #f1f5f9;
  border-color: #94a3b8;
  color: #0f172a;
}

.page-active {
  background: #0A2A5E !important;
  color: #ffffff !important;
  border-color: #0A2A5E !important;
  box-shadow: 0 2px 6px rgba(10, 42, 94, 0.25);
  font-weight: 800;
}

/* ESTADO VACÍO */
.empty-state-cell {
  padding: 48px 20px;
  text-align: center;
}

.empty-state-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
}

.empty-icon {
  font-size: 36px;
}

.empty-title {
  font-size: 16px;
  font-weight: 800;
  color: #0f172a;
  margin: 0;
}

.empty-sub {
  font-size: 13px;
  color: #64748b;
  margin: 0;
}

/* MODALES PROFESIONALES */
.modal-backdrop {
  position: fixed;
  inset: 0;
  background-color: rgba(15, 23, 42, 0.65);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 100;
  padding: 20px;
}

.modal-card {
  background: white;
  border-radius: 16px;
  width: 100%;
  max-width: 480px;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
  overflow: hidden;
  animation: modalEnter 0.2s ease-out;
}

.modal-wide {
  max-width: 720px;
}

@keyframes modalEnter {
  from { opacity: 0; transform: scale(0.95); }
  to { opacity: 1; transform: scale(1); }
}

.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 20px;
  border-bottom: 1px solid #e2e8f0;
  background: #f8fafc;
}

.modal-header-tabs {
  display: flex;
  gap: 8px;
}

.modal-tab-btn {
  background: transparent;
  border: none;
  padding: 8px 14px;
  border-radius: 8px;
  font-size: 13px;
  font-weight: 700;
  color: #64748b;
  cursor: pointer;
  transition: all 0.2s ease;
}

.modal-tab-btn:hover {
  background: #f1f5f9;
  color: #0f172a;
}

.tab-active {
  background: white !important;
  color: #0A2A5E !important;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  border: 1px solid #e2e8f0;
}

.modal-title {
  font-size: 17px;
  font-weight: 800;
  color: #0A2A5E;
  margin: 0;
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
  color: #0f172a;
}

.modal-body {
  padding: 22px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  max-height: 75vh;
  overflow-y: auto;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 14px;
}

.form-label {
  font-size: 12.5px;
  font-weight: 700;
  color: #334155;
}

.form-input {
  padding: 10px 14px;
  border: 1.5px solid #e2e8f0;
  border-radius: 8px;
  font-size: 13.5px;
  color: #1e293b;
  outline: none;
  background: #f8fafc;
  transition: all 0.2s ease;
}

.form-input:focus {
  background: white;
  border-color: #16a34a;
  box-shadow: 0 0 0 3px rgba(22, 163, 74, 0.15);
}

.form-textarea-small {
  height: 70px;
  resize: vertical;
}

/* SECCIÓN DE ARCHIVO ADJUNTO */
.attachment-section {
  border: 1px dashed #cbd5e1;
  background: #f8fafc;
  border-radius: 12px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.current-file-box {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: white;
  border: 1px solid #e2e8f0;
  border-radius: 10px;
  padding: 12px 14px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.04);
}

.file-info-left {
  display: flex;
  align-items: center;
  gap: 10px;
}

.file-type-icon {
  font-size: 20px;
}

.attached-file-name {
  font-size: 13.5px;
  font-weight: 700;
  color: #0f172a;
  display: block;
}

.attached-source-tag {
  font-size: 11px;
  font-weight: 600;
  color: #2563eb;
  background: #eff6ff;
  padding: 1px 6px;
  border-radius: 4px;
  display: inline-block;
  margin-top: 2px;
}

.btn-remove-attachment {
  display: inline-flex;
  align-items: center;
  background: #fee2e2;
  color: #b91c1c;
  border: 1px solid #fecaca;
  padding: 6px 12px;
  border-radius: 6px;
  font-size: 12px;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn-remove-attachment:hover {
  background: #dc2626;
  color: white;
}

/* OPCIONES DE SUBIDA (LOCAL O WEB) */
.upload-options-container {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.upload-tabs-selector {
  display: flex;
  gap: 8px;
}

.upload-tab-btn {
  flex: 1;
  padding: 8px 12px;
  border: 1px solid #cbd5e1;
  background: white;
  border-radius: 6px;
  font-size: 12.5px;
  font-weight: 700;
  color: #475569;
  cursor: pointer;
  transition: all 0.2s ease;
}

.active-upload-tab {
  background: #0A2A5E !important;
  color: white !important;
  border-color: #0A2A5E !important;
}

.local-upload-dropzone {
  position: relative;
  border: 2px dashed #94a3b8;
  border-radius: 10px;
  padding: 20px;
  text-align: center;
  background: white;
  cursor: pointer;
  transition: border-color 0.2s ease;
}

.local-upload-dropzone:hover {
  border-color: #16a34a;
}

.hidden-file-input {
  position: absolute;
  inset: 0;
  opacity: 0;
  cursor: pointer;
}

.dropzone-label {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  cursor: pointer;
}

.dropzone-icon {
  font-size: 28px;
}

.dropzone-text {
  font-size: 13.5px;
  font-weight: 700;
  color: #0A2A5E;
}

.dropzone-sub {
  font-size: 11px;
  color: #64748b;
}

.web-url-upload-box {
  display: flex;
  gap: 8px;
}

.btn-attach-web {
  background: #0A2A5E;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 8px;
  font-size: 13px;
  font-weight: 700;
  cursor: pointer;
  white-space: nowrap;
}

.btn-attach-web:hover {
  background: #1e3a8a;
}

/* EDITOR DE TEXTO ESTILO MICROSOFT WORD */
.tab-content-word {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.word-ribbon-toolbar {
  background: #f1f5f9;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  padding: 6px 12px;
  display: flex;
  align-items: center;
  gap: 8px;
  flex-wrap: wrap;
}

.toolbar-group {
  display: flex;
  gap: 4px;
}

.ribbon-btn {
  background: white;
  border: 1px solid #cbd5e1;
  border-radius: 4px;
  padding: 4px 10px;
  font-size: 12px;
  font-weight: 700;
  color: #334155;
  cursor: pointer;
  transition: all 0.15s ease;
}

.ribbon-btn:hover {
  background: #e2e8f0;
  color: #0f172a;
}

.btn-clear-text {
  color: #dc2626;
  border-color: #fecaca;
  background: #fef2f2;
}

.btn-clear-text:hover {
  background: #fee2e2;
}

.toolbar-divider {
  width: 1px;
  height: 20px;
  background: #cbd5e1;
  margin: 0 4px;
}

.toolbar-status-badge {
  margin-left: auto;
  font-size: 11px;
  font-weight: 700;
  color: #0A2A5E;
  background: #e0f2fe;
  padding: 2px 8px;
  border-radius: 4px;
}

/* LIENZO DE HOJA WORD */
.word-canvas-wrapper {
  background: #e2e8f0;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  padding: 16px 20px 10px 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.word-ruler {
  font-family: monospace;
  font-size: 10px;
  color: #94a3b8;
  letter-spacing: 2px;
  margin-bottom: 8px;
}

.word-paper-sheet {
  background: white;
  width: 100%;
  max-width: 620px;
  border-radius: 4px;
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.12), 0 1px 3px rgba(0, 0, 0, 0.08);
  border: 1px solid #cbd5e1;
  padding: 24px;
}

.word-paper-textarea {
  width: 100%;
  height: 240px;
  border: none;
  outline: none;
  resize: vertical;
  font-family: 'Georgia', 'Times New Roman', serif;
  font-size: 14.5px;
  line-height: 1.6;
  color: #0f172a;
  background: transparent;
}

.word-status-footer {
  display: flex;
  justify-content: space-between;
  width: 100%;
  max-width: 620px;
  font-size: 11px;
  font-weight: 600;
  color: #64748b;
  margin-top: 10px;
  padding: 0 4px;
}

.word-badge-lang {
  color: #0A2A5E;
  font-weight: 700;
}

.modal-footer {
  padding: 16px 24px;
  background: #f8fafc;
  border-top: 1px solid #e2e8f0;
  display: flex;
  justify-content: flex-end;
  gap: 10px;
}

.btn-secondary {
  padding: 9px 16px;
  border: 1px solid #cbd5e1;
  background: white;
  color: #475569;
  border-radius: 8px;
  font-size: 13px;
  font-weight: 700;
  cursor: pointer;
}

.btn-secondary:hover {
  background: #f1f5f9;
}

.btn-primary {
  padding: 9px 18px;
  border: none;
  background: #16a34a;
  color: white;
  border-radius: 8px;
  font-size: 13px;
  font-weight: 700;
  cursor: pointer;
  box-shadow: 0 2px 6px rgba(22, 163, 74, 0.3);
}

.btn-primary:hover {
  background: #15803d;
}

/* ========================================================
   ESTILOS ULTRA-PROFESIONALES: MODAL ADJUNTAR DOCUMENTO
   ======================================================== */
.modal-pro-card {
  max-width: 580px !important;
  border-radius: 20px !important;
  box-shadow: 0 25px 60px -15px rgba(10, 42, 94, 0.35), 0 10px 20px -5px rgba(0, 0, 0, 0.08) !important;
  overflow: hidden;
  border: 1px solid rgba(226, 232, 240, 0.9);
}

.modal-pro-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 18px 24px;
  background: linear-gradient(135deg, #0A2A5E 0%, #173b75 100%);
  color: white;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.modal-header-brand {
  display: flex;
  align-items: center;
  gap: 14px;
}

.modal-badge-icon {
  width: 44px;
  height: 44px;
  border-radius: 12px;
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(16, 185, 129, 0.35);
  flex-shrink: 0;
}

.modal-header-desc {
  font-size: 12px;
  color: #94a3b8;
  margin: 3px 0 0 0;
  font-weight: 500;
}

.modal-close-btn-pro {
  background: rgba(255, 255, 255, 0.1);
  border: none;
  font-size: 16px;
  color: #e2e8f0;
  cursor: pointer;
  width: 34px;
  height: 34px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
}

.modal-close-btn-pro:hover {
  background: rgba(255, 255, 255, 0.25);
  color: white;
  transform: scale(1.05);
}

.modal-pro-body {
  padding: 22px 24px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  max-height: calc(85vh - 130px);
  overflow-y: auto;
}

.input-with-icon {
  position: relative;
  display: flex;
  align-items: center;
}

.input-icon {
  position: absolute;
  left: 12px;
  font-size: 15px;
  pointer-events: none;
}

.input-padded {
  padding-left: 38px !important;
  width: 100%;
}

.label-required {
  color: #ef4444;
  margin-left: 4px;
}

.upload-pro-box {
  background: #f8fafc;
  border: 1.5px solid #e2e8f0;
  border-radius: 14px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.upload-pro-header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}

.upload-pro-title {
  font-size: 13px;
  font-weight: 800;
  color: #0A2A5E;
}

.upload-pro-sub {
  font-size: 11.5px;
  color: #64748b;
  font-weight: 500;
}

.upload-method-selector {
  display: flex;
  background: #e2e8f0;
  padding: 3px;
  border-radius: 10px;
  gap: 4px;
}

.upload-method-tab {
  flex: 1;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 8px 12px;
  border: none;
  background: transparent;
  border-radius: 8px;
  font-size: 12px;
  font-weight: 700;
  color: #475569;
  cursor: pointer;
  transition: all 0.2s ease;
}

.upload-method-tab:hover {
  color: #0f172a;
}

.active-method {
  background: white !important;
  color: #0A2A5E !important;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
  font-weight: 800;
}

.local-dropzone-pro {
  border: 2px dashed #93c5fd;
  background: #ffffff;
  border-radius: 12px;
  padding: 20px 16px;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s ease;
  position: relative;
}

.local-dropzone-pro:hover {
  border-color: #2563eb;
  background: #f0f7ff;
  transform: translateY(-1px);
}

.dropzone-label-pro {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  cursor: pointer;
}

.dropzone-icon-circle {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: #ecfdf5;
  border: 1px solid #a7f3d0;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 10px rgba(16, 185, 129, 0.15);
}

.dropzone-main-text {
  font-size: 13.5px;
  font-weight: 700;
  color: #1e293b;
  display: block;
}

.dropzone-hint {
  font-size: 11.5px;
  color: #64748b;
  margin-top: 2px;
  display: block;
}

.web-url-pro-box {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.web-input-group {
  display: flex;
  gap: 8px;
  align-items: center;
}

.web-input-icon {
  font-size: 16px;
}

.web-input-field {
  flex: 1;
}

.btn-link-web {
  background: #0A2A5E;
  color: white;
  font-weight: 700;
  font-size: 13px;
  padding: 10px 18px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  transition: background 0.2s ease;
  white-space: nowrap;
}

.btn-link-web:hover:not(:disabled) {
  background: #173b75;
}

.btn-link-web:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.web-helper-text {
  font-size: 11px;
  color: #64748b;
  line-height: 1.4;
  margin: 0;
}

.attached-file-preview-card {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border: 1.5px solid #bbf7d0;
  background: #f0fdf4;
  border-radius: 10px;
  padding: 12px 14px;
  box-shadow: 0 2px 8px rgba(16, 185, 129, 0.1);
}

.file-preview-badge {
  width: 40px;
  height: 40px;
  border-radius: 8px;
  background: #15803d;
  color: white;
  font-size: 11px;
  font-weight: 900;
  display: flex;
  align-items: center;
  justify-content: center;
  letter-spacing: 0.5px;
  flex-shrink: 0;
}

.file-preview-details {
  flex: 1;
  margin: 0 12px;
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.file-preview-name {
  font-size: 13.5px;
  font-weight: 800;
  color: #14532d;
  word-break: break-all;
}

.file-preview-meta {
  display: flex;
  align-items: center;
  gap: 8px;
  flex-wrap: wrap;
}

.file-preview-tag {
  font-size: 11px;
  font-weight: 600;
  color: #2563eb;
  background: #eff6ff;
  padding: 1px 6px;
  border-radius: 4px;
}

.file-preview-size {
  font-size: 11.5px;
  color: #64748b;
  font-weight: 600;
}

.file-ready-tag {
  font-size: 11px;
  font-weight: 700;
  color: #16a34a;
  background: #dcfce7;
  padding: 1px 6px;
  border-radius: 4px;
}

.btn-change-file {
  background: white;
  border: 1px solid #fca5a5;
  color: #dc2626;
  font-size: 11.5px;
  font-weight: 700;
  padding: 6px 10px;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.2s ease;
  white-space: nowrap;
}

.btn-change-file:hover {
  background: #fee2e2;
}

.label-with-counter {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}

.text-counter {
  font-size: 11.5px;
  color: #64748b;
  font-weight: 600;
}

.form-textarea-modern {
  height: 75px;
  resize: vertical;
  font-family: inherit;
  font-size: 13px;
  width: 100%;
}

.modal-pro-footer {
  display: flex;
  justify-content: flex-end;
  gap: 12px;
  padding: 16px 24px;
  background: #f8fafc;
  border-top: 1px solid #e2e8f0;
}

.btn-primary-action {
  display: inline-flex;
  align-items: center;
  background: linear-gradient(135deg, #16a34a 0%, #15803d 100%);
  color: white;
  font-weight: 800;
  font-size: 13.5px;
  padding: 10px 20px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(22, 163, 74, 0.35);
  transition: all 0.2s ease;
}

.btn-primary-action:hover {
  background: linear-gradient(135deg, #15803d 0%, #166534 100%);
  transform: translateY(-1px);
  box-shadow: 0 6px 16px rgba(22, 163, 74, 0.45);
}

/* ========================================================
   ESTILOS 3D ULTRA-PROFESIONALES: MODAL EDITAR DOCUMENTO
   ======================================================== */
.modal-3d-container {
  max-width: 760px !important;
  border-radius: 22px !important;
  box-shadow: 
    0 35px 70px -15px rgba(10, 42, 94, 0.45),
    0 15px 30px -5px rgba(0, 0, 0, 0.12),
    inset 0 1px 1px rgba(255, 255, 255, 0.8) !important;
  border: 1px solid rgba(226, 232, 240, 0.95);
  overflow: hidden;
  perspective: 1000px;
}

.modal-3d-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 24px;
  background: linear-gradient(135deg, #0A2A5E 0%, #173b75 55%, #0d2650 100%);
  color: white;
  border-bottom: 2px solid rgba(15, 23, 42, 0.2);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.modal-3d-brand {
  display: flex;
  align-items: center;
  gap: 12px;
}

.modal-3d-title {
  font-size: 18px;
  font-weight: 900;
  color: #ffffff !important;
  margin: 0;
  letter-spacing: 0.3px;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.4);
}

.modal-pro-title-clean {
  font-size: 18px;
  font-weight: 900;
  color: #ffffff !important;
  margin: 0;
  letter-spacing: 0.3px;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.4);
}

.modal-3d-icon-badge {
  width: 42px;
  height: 42px;
  border-radius: 12px;
  background: linear-gradient(145deg, #3b82f6 0%, #1d4ed8 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 
    0 4px 10px rgba(37, 99, 235, 0.4),
    inset 0 1px 1px rgba(255, 255, 255, 0.5),
    inset 0 -2px 4px rgba(0, 0, 0, 0.2);
  flex-shrink: 0;
}

.modal-3d-doc-tag {
  display: inline-block;
  font-size: 11.5px;
  color: #93c5fd;
  font-weight: 600;
  margin-top: 1px;
}

.modal-3d-tabs {
  display: flex;
  background: rgba(15, 23, 42, 0.35);
  padding: 4px;
  border-radius: 12px;
  gap: 6px;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.3);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.modal-3d-tab-btn {
  background: transparent;
  border: none;
  padding: 8px 16px;
  border-radius: 8px;
  font-size: 12.5px;
  font-weight: 700;
  color: #cbd5e1;
  cursor: pointer;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
  display: inline-flex;
  align-items: center;
}

.modal-3d-tab-btn:hover {
  color: white;
}

.tab-3d-active {
  background: white !important;
  color: #0A2A5E !important;
  font-weight: 800 !important;
  box-shadow: 
    0 4px 12px rgba(0, 0, 0, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 1) !important;
  transform: translateY(-1px);
}

.modal-3d-body {
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 18px;
  max-height: calc(85vh - 140px);
  overflow-y: auto;
  background: #fdfefe;
}

.form-label-3d {
  font-size: 12.5px;
  font-weight: 800;
  color: #1e293b;
  letter-spacing: 0.2px;
}

.input-3d-wrapper {
  position: relative;
  display: flex;
  align-items: center;
}

.input-3d-icon {
  position: absolute;
  left: 12px;
  font-size: 15px;
  pointer-events: none;
}

.form-input-3d {
  width: 100%;
  padding: 10px 14px 10px 38px;
  border: 1.5px solid #cbd5e1;
  border-radius: 10px;
  font-size: 13.5px;
  color: #0f172a;
  outline: none;
  background: #ffffff;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.04);
  transition: all 0.2s ease;
}

.form-input-3d:focus {
  border-color: #2563eb;
  background: #ffffff;
  box-shadow: 
    0 0 0 3px rgba(37, 99, 235, 0.15),
    inset 0 1px 2px rgba(0, 0, 0, 0.02);
}

.select-3d {
  padding-left: 14px !important;
  cursor: pointer;
}

.attachment-section-3d {
  background: linear-gradient(180deg, #f8fafc 0%, #f1f5f9 100%);
  border: 1.5px solid #cbd5e1;
  border-radius: 14px;
  padding: 18px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  box-shadow: 
    0 2px 6px rgba(0, 0, 0, 0.03),
    inset 0 1px 0 rgba(255, 255, 255, 0.8);
}

.attachment-header-3d {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}

.attachment-title-3d {
  font-size: 13px;
  font-weight: 800;
  color: #0A2A5E;
}

.attachment-sub-3d {
  font-size: 11px;
  font-weight: 600;
  color: #16a34a;
}

.file-card-3d {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: white;
  border: 1.5px solid #93c5fd;
  border-radius: 12px;
  padding: 12px 16px;
  box-shadow: 
    0 6px 16px rgba(15, 23, 42, 0.08),
    inset 0 1px 0 #ffffff;
}

.file-card-3d-badge {
  width: 42px;
  height: 42px;
  border-radius: 10px;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
  font-size: 11px;
  font-weight: 900;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 8px rgba(37, 99, 235, 0.35);
  flex-shrink: 0;
}

.file-card-3d-info {
  flex: 1;
  margin: 0 14px;
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.file-card-3d-name {
  font-size: 13.5px;
  font-weight: 800;
  color: #0f172a;
}

.file-card-3d-meta {
  display: flex;
  align-items: center;
  gap: 8px;
}

.file-card-3d-tag {
  font-size: 11px;
  font-weight: 700;
  color: #2563eb;
  background: #eff6ff;
  padding: 1px 7px;
  border-radius: 4px;
}

.file-card-3d-check {
  font-size: 11px;
  font-weight: 700;
  color: #16a34a;
}

.btn-3d-remove {
  display: inline-flex;
  align-items: center;
  background: linear-gradient(180deg, #fee2e2 0%, #fecaca 100%);
  color: #b91c1c;
  border: 1px solid #f87171;
  padding: 7px 14px;
  border-radius: 8px;
  font-size: 12px;
  font-weight: 800;
  cursor: pointer;
  box-shadow: 
    0 2px 4px rgba(220, 38, 38, 0.15),
    inset 0 1px 0 rgba(255, 255, 255, 0.7);
  transition: all 0.2s ease;
}

.btn-3d-remove:hover {
  background: linear-gradient(180deg, #dc2626 0%, #b91c1c 100%);
  color: white;
  border-color: #991b1b;
  box-shadow: 0 4px 10px rgba(220, 38, 38, 0.35);
  transform: translateY(-1px);
}

/* 3D Word Ribbon */
.word-ribbon-toolbar-3d {
  background: linear-gradient(180deg, #f8fafc 0%, #e2e8f0 100%);
  border: 1px solid #cbd5e1;
  border-radius: 10px;
  padding: 8px 12px;
  display: flex;
  align-items: center;
  gap: 8px;
  box-shadow: 
    0 2px 4px rgba(0, 0, 0, 0.05),
    inset 0 1px 0 #ffffff;
}

.ribbon-btn-3d {
  background: white;
  border: 1px solid #cbd5e1;
  border-radius: 6px;
  padding: 5px 12px;
  font-size: 12px;
  font-weight: 800;
  color: #334155;
  cursor: pointer;
  box-shadow: 
    0 2px 0 #cbd5e1,
    0 2px 4px rgba(0, 0, 0, 0.05);
  transition: all 0.15s ease;
}

.ribbon-btn-3d:hover {
  background: #f8fafc;
  color: #0f172a;
  transform: translateY(-1px);
  box-shadow: 0 3px 0 #cbd5e1, 0 3px 6px rgba(0, 0, 0, 0.08);
}

.ribbon-btn-3d:active {
  transform: translateY(1px);
  box-shadow: 0 1px 0 #cbd5e1;
}

.toolbar-divider-3d {
  width: 1px;
  height: 22px;
  background: #cbd5e1;
  box-shadow: 1px 0 0 rgba(255, 255, 255, 0.8);
}

.btn-clear-3d {
  color: #dc2626 !important;
  border-color: #fca5a5 !important;
}

.toolbar-status-badge-3d {
  margin-left: auto;
  font-size: 11px;
  font-weight: 800;
  color: #16a34a;
  background: #dcfce7;
  padding: 4px 10px;
  border-radius: 6px;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.8);
}

.word-canvas-wrapper-3d {
  background: #e2e8f0;
  border-radius: 12px;
  padding: 16px;
  box-shadow: inset 0 2px 6px rgba(0, 0, 0, 0.08);
}

.word-paper-sheet-3d {
  background: #ffffff;
  border-radius: 4px;
  box-shadow: 
    0 12px 28px rgba(15, 23, 42, 0.15),
    0 2px 6px rgba(15, 23, 42, 0.08);
  min-height: 240px;
  border: 1px solid #cbd5e1;
  display: flex;
}

.word-paper-textarea-3d {
  width: 100%;
  min-height: 240px;
  border: none;
  outline: none;
  padding: 24px 28px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 13.5px;
  line-height: 1.7;
  color: #0f172a;
  background: transparent;
  resize: vertical;
}

.word-status-footer-3d {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 8px 12px 0 12px;
  font-size: 11.5px;
  color: #64748b;
  font-weight: 600;
}

.modal-3d-footer {
  display: flex;
  justify-content: flex-end;
  gap: 12px;
  padding: 16px 24px;
  background: linear-gradient(180deg, #f8fafc 0%, #f1f5f9 100%);
  border-top: 1.5px solid #e2e8f0;
  box-shadow: 0 -2px 6px rgba(0, 0, 0, 0.03);
}

.btn-3d-secondary {
  padding: 10px 18px;
  background: white;
  border: 1px solid #cbd5e1;
  border-radius: 10px;
  font-size: 13px;
  font-weight: 700;
  color: #475569;
  cursor: pointer;
  box-shadow: 
    0 2px 0 #cbd5e1,
    0 2px 4px rgba(0, 0, 0, 0.05);
  transition: all 0.15s ease;
}

.btn-3d-secondary:hover {
  background: #f8fafc;
  color: #0f172a;
  transform: translateY(-1px);
}

.btn-3d-secondary:active {
  transform: translateY(1px);
  box-shadow: 0 1px 0 #cbd5e1;
}

.btn-3d-primary {
  display: inline-flex;
  align-items: center;
  background: linear-gradient(180deg, #16a34a 0%, #15803d 100%);
  color: white;
  font-weight: 800;
  font-size: 13.5px;
  padding: 10px 22px;
  border-radius: 10px;
  border: none;
  cursor: pointer;
  box-shadow: 
    0 4px 0 #14532d,
    0 6px 14px rgba(22, 163, 74, 0.4),
    inset 0 1px 0 rgba(255, 255, 255, 0.35);
  transition: all 0.15s ease;
}

.btn-3d-primary:hover {
  background: linear-gradient(180deg, #15803d 0%, #166534 100%);
  transform: translateY(-1px);
  box-shadow: 
    0 5px 0 #14532d,
    0 8px 18px rgba(22, 163, 74, 0.5);
}

.btn-3d-primary:active {
  transform: translateY(2px);
  box-shadow: 
    0 2px 0 #14532d,
    0 3px 6px rgba(22, 163, 74, 0.3);
}

/* ========================================================
   ESTILOS DE VISUALIZADOR DE DOCUMENTO EN FORMATO A4
   ======================================================== */
.btn-view-icon {
  background-color: #ecfdf5;
  color: #059669;
  border-color: #a7f3d0;
}

.btn-view-icon:hover {
  background-color: #059669;
  color: white;
  border-color: #059669;
  transform: translateY(-1px);
  box-shadow: 0 4px 10px rgba(5, 150, 105, 0.25);
}

.modal-a4-backdrop {
  z-index: 150 !important;
  background-color: rgba(10, 25, 47, 0.85) !important;
  backdrop-filter: blur(8px) !important;
  padding: 16px !important;
  display: flex !important;
  align-items: center !important;
  justify-content: center !important;
}

.a4-viewer-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  max-width: 840px;
  max-height: 94vh;
  margin: auto;
  animation: modalEnter 0.25s ease-out;
}

.a4-viewer-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  max-width: 794px;
  padding: 12px 20px;
  background: #0A2A5E;
  border-radius: 14px 14px 0 0;
  color: white;
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.25);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.a4-header-left {
  display: flex;
  align-items: center;
  gap: 10px;
  flex-wrap: wrap;
}

.a4-doc-badge {
  background: rgba(255, 255, 255, 0.15);
  font-size: 10.5px;
  font-weight: 800;
  letter-spacing: 0.5px;
  padding: 3px 8px;
  border-radius: 4px;
  color: #93c5fd;
}

.a4-doc-title {
  font-size: 15px;
  font-weight: 800;
  color: #ffffff;
}

.a4-header-actions {
  display: flex;
  align-items: center;
  gap: 10px;
}

.btn-a4-action {
  display: inline-flex;
  align-items: center;
  padding: 6px 14px;
  background: rgba(255, 255, 255, 0.15);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 8px;
  font-size: 12.5px;
  font-weight: 700;
  color: white;
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn-a4-action:hover {
  background: rgba(255, 255, 255, 0.28);
  transform: translateY(-1px);
}

.a4-close-btn {
  background: transparent;
  border: none;
  font-size: 18px;
  color: #cbd5e1;
  cursor: pointer;
  width: 32px;
  height: 32px;
  border-radius: 6px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
}

.a4-close-btn:hover {
  background: rgba(255, 255, 255, 0.2);
  color: white;
}

.a4-sheet-scroll-area {
  width: 100%;
  max-width: 794px;
  display: flex;
  justify-content: center;
  max-height: calc(94vh - 65px);
  overflow-y: auto;
  padding: 24px 0 32px 0;
  background: #334155;
  border-radius: 0 0 14px 14px;
  box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.3);
}

/* HOJA REAL CON MEDIDAS EXACTAS DE PROPORCIÓN A4 (1 : 1.414) */
.a4-paper-page {
  width: 720px;
  min-height: 1018px;
  background: #ffffff;
  border-radius: 2px;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.45), 0 2px 6px rgba(0, 0, 0, 0.15);
  padding: 56px 60px;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  color: #1e293b;
  overflow: hidden;
}

.a4-watermark {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) rotate(-35deg);
  font-size: 54px;
  font-weight: 900;
  color: rgba(10, 42, 94, 0.035);
  letter-spacing: 8px;
  pointer-events: none;
  user-select: none;
  z-index: 1;
  white-space: nowrap;
}

.a4-official-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  z-index: 2;
  margin-bottom: 16px;
}

.a4-header-emblem {
  display: flex;
  align-items: center;
  gap: 12px;
}

.a4-emblem-circle {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  border: 2px solid #0A2A5E;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 22px;
  background: #f8fafc;
}

.a4-emblem-text {
  display: flex;
  flex-direction: column;
}

.a4-gov-title {
  font-size: 12px;
  font-weight: 900;
  color: #0A2A5E;
  letter-spacing: 0.5px;
}

.a4-gov-sub {
  font-size: 10.5px;
  font-weight: 700;
  color: #64748b;
}

.a4-folio-box {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.a4-folio-label {
  font-size: 9.5px;
  font-weight: 800;
  color: #64748b;
  letter-spacing: 0.5px;
}

.a4-folio-val {
  font-size: 11.5px;
  font-weight: 800;
  color: #0A2A5E;
  font-family: monospace;
}

.a4-date-stamp {
  font-size: 10.5px;
  color: #475569;
  margin-top: 2px;
}

.a4-divider-double {
  border-top: 3px double #cbd5e1;
  margin-bottom: 24px;
  z-index: 2;
}

.a4-title-section {
  text-align: center;
  margin-bottom: 28px;
  z-index: 2;
}

.a4-type-badge {
  display: inline-block;
  font-size: 11px;
  font-weight: 800;
  color: #2563eb;
  background: #eff6ff;
  border: 1px solid #bfdbfe;
  padding: 2px 10px;
  border-radius: 4px;
  letter-spacing: 1px;
  margin-bottom: 8px;
}

.a4-main-heading {
  font-size: 22px;
  font-weight: 900;
  color: #0f172a;
  margin: 4px 0 6px 0;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.a4-status-declaration {
  font-size: 11px;
  font-weight: 700;
  color: #16a34a;
  letter-spacing: 0.5px;
  display: block;
}

.a4-content-body {
  flex: 1;
  z-index: 2;
  line-height: 1.8;
  font-size: 14px;
  color: #334155;
  margin-bottom: 28px;
  text-align: justify;
}

.a4-paragraph {
  margin-bottom: 14px;
  white-space: pre-line;
}

.a4-attached-meta {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #f8fafc;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  padding: 10px 14px;
  margin-bottom: 24px;
  z-index: 2;
}

.a4-attached-left {
  display: flex;
  align-items: center;
  gap: 8px;
}

.a4-attached-icon {
  font-size: 16px;
}

.a4-attached-name {
  font-size: 12px;
  font-weight: 800;
  color: #0f172a;
  display: block;
}

.a4-attached-source {
  font-size: 10.5px;
  color: #64748b;
  font-weight: 600;
}

.a4-hash-badge {
  font-size: 10.5px;
  font-family: monospace;
  color: #64748b;
  background: #e2e8f0;
  padding: 2px 6px;
  border-radius: 4px;
}

.a4-official-footer {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  padding-top: 20px;
  border-top: 1px solid #e2e8f0;
  z-index: 2;
  margin-bottom: 20px;
}

.a4-signature-box {
  display: flex;
  flex-direction: column;
  width: 260px;
}

.a4-signature-line {
  width: 180px;
  height: 1.5px;
  background: #334155;
  margin-bottom: 6px;
}

.a4-sign-name {
  font-size: 10.5px;
  font-weight: 800;
  color: #0f172a;
}

.a4-sign-role {
  font-size: 10px;
  color: #64748b;
}

.a4-seal-box {
  display: flex;
  align-items: center;
  gap: 10px;
  border: 1.5px dashed #059669;
  padding: 6px 10px;
  border-radius: 8px;
  background: #f0fdf4;
}

.a4-qr-mock {
  width: 34px;
  height: 34px;
  border: 1.5px solid #059669;
  background: white;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.qr-pattern {
  width: 20px;
  height: 20px;
  background: repeating-linear-gradient(45deg, #059669 0px, #059669 2px, white 2px, white 4px);
}

.qr-text {
  font-size: 5px;
  font-weight: 900;
  color: #059669;
}

.a4-seal-text {
  display: flex;
  flex-direction: column;
  font-size: 9.5px;
  font-weight: 800;
  color: #065f46;
}

.a4-bottom-page-number {
  text-align: center;
  font-size: 10px;
  color: #94a3b8;
  font-weight: 500;
  z-index: 2;
}

/* RESPONSIVE PANEL */
@media (max-width: 960px) {
  .dashboard-layout {
    flex-direction: column;
    gap: 24px;
  }
  .stats-sidebar {
    width: 100%;
  }
  .content-header-row {
    flex-direction: column;
    align-items: flex-start;
  }
  .table-container-pro {
    overflow-x: auto;
  }
  .docs-table-pro {
    min-width: 600px;
  }
}

@media (max-width: 768px) {
  .container {
    padding: 16px 12px;
    max-width: 100%;
  }
  .filter-controls-pro {
    flex-direction: column;
    align-items: stretch;
  }
  .results-badge {
    margin-left: 0;
  }
}
</style>
