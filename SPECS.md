# SPECS — AgentHub Admin Panel (Prototipo HTML)

## 1) Descripción breve del producto

AgentHub es una plataforma SaaS donde empresas alquilan agentes de IA preconfigurados para resolver tareas de negocio. Cada agente puede incorporar distintas skills (por ejemplo: navegación web, lectura de documentos o gestión de calendarios) según el caso de uso.

El usuario objetivo de este prototipo es el administrador interno de AgentHub (equipo operativo/producto), que necesita:
- visualizar métricas clave del negocio,
- gestionar usuarios, agentes y skills,
- revisar contrataciones,
- monitorear y resolver errores de ejecución.

## 2) Stack tecnológico y restricciones

### Stack obligatorio
- Estructura: HTML5 semántico (un solo prototipo navegable con secciones).
- Estilos: Tailwind CSS cargado por CDN.
- Interactividad: JavaScript vanilla (sin librerías auxiliares).

### Restricciones
- No usar frameworks de frontend (React, Vue, Angular, Svelte, etc.).
- No usar backend, base de datos ni llamadas a APIs.
- Todos los datos mostrados serán hardcodeados de forma realista.
- El prototipo debe ser responsive (desktop-first con adaptación móvil).
- Soporte de modo claro/oscuro global mediante clases `dark:` de Tailwind y un toggle en la topbar.
- Navegación lateral persistente visible en desktop y accesible en móvil.

## 3) Especificaciones por sección

## 3.1 Dashboard

1. **Grid de métricas (4 tarjetas)**
- Componente: cuatro tarjetas de métrica en grid responsive.
- Contenido por tarjeta: icono, etiqueta y valor hardcodeado.
- Métricas requeridas: ingresos totales del mes, pérdida por descuentos/cupones, agentes activos, agentes fallando.
- Comportamiento visual: 2x2 en pantallas medianas/grandes; 1 columna en móvil.

2. **Identidad visual de cada métrica**
- Cada tarjeta usa color de acento diferenciado por tipo (éxito, advertencia, neutro, error).
- Las tarjetas incluyen borde suave, sombra ligera y jerarquía tipográfica clara.
- En modo oscuro se mantienen contraste AA mínimo y legibilidad del valor principal.

3. **Placeholder de gráfico semanal**
- Debajo del grid, incluir un bloque full-width como placeholder de gráfico de actividad semanal.
- Estilo: borde discontinuo, altura mínima definida, etiqueta centrada "Actividad semanal (placeholder)".
- Debe conservar proporciones en responsive y adaptarse a tema claro/oscuro.

4. **Espaciado y escaneo visual**
- La sección debe tener título, subtítulo contextual y separación vertical consistente.
- Las tarjetas y el placeholder deben alinearse al mismo ancho de contenedor.
- Debe priorizar lectura de arriba hacia abajo en menos de 5 segundos.

## 3.2 Gestión de usuarios

1. **Tabla principal de usuarios**
- Columnas obligatorias: Nombre, Email, Plan, Estado, Acciones.
- Mínimo 6 filas de datos hardcodeados para simular volumen real.
- Encabezado sticky opcional, pero filas con hover visible y zebra suave opcional.

2. **Dropdown de acciones por fila**
- Botón disparador: icono `⋮` por fila.
- Opciones mínimas: "Ver detalle" y "Eliminar".
- Comportamiento: abrir/cerrar por click; cerrar al hacer click fuera; solo un dropdown abierto a la vez.

3. **Modal de detalle de usuario**
- Acción "Ver detalle" abre modal overlay centrado con backdrop semitransparente.
- El modal muestra ficha completa hardcodeada (nombre, email, plan, estado, fecha alta, última actividad).
- Debe cerrarse con botón de cierre y también al hacer click sobre backdrop.

4. **Estados de usuario como badge**
- El estado (activo, suspendido, trial, etc.) debe mostrarse como badge con color consistente.
- Colores deben mapear semántica (activo=verde, suspendido=rojo/ámbar, trial=azul).
- Badges deben conservar legibilidad en dark mode.

## 3.3 Gestión de agentes

1. **Listado de agentes con información clave**
- Mostrar por ítem: nombre del agente, propietario/cliente, estado (activo/inactivo/fallando), skills asociadas (colapsadas por defecto), acciones.
- Mínimo 6 agentes hardcodeados.
- Cada ítem debe tener separación visual tipo card o fila elevada.

2. **Lista de skills colapsable por agente**
- Las skills comienzan ocultas y se expanden con control explícito (botón o chevron).
- Al expandir, mostrar lista de skills como chips/badges.
- La transición debe ser suave (animación de altura/opacidad) para comunicar cambio de estado.

3. **Dropdown de acciones por agente**
- Botón `⋮` por agente con opciones "Configurar" y "Eliminar".
- "Configurar" abre modal con el prompt de sistema del agente (texto hardcodeado extenso).
- Dropdown respeta reglas globales: click fuera cierra, un solo menú abierto.

4. **Semántica visual de estado de agente**
- Estado debe aparecer como badge codificado por color.
- `fallando` debe resaltar más que `inactivo` para priorizar atención.
- En modo oscuro, badges mantienen contraste y no dependen solo del color (texto explícito).

## 3.4 Skills

1. **Contexto de la sección**
- Incluir texto explicativo breve al inicio: qué es una skill en AgentHub y para qué se adjunta a un agente.
- Este bloque debe diferenciarse visualmente (callout con fondo suave y borde).
- Contenido breve (2–4 líneas) orientado a administración interna.

2. **Catálogo de skills**
- Cada skill debe mostrar: nombre, descripción breve y contador de agentes con esa skill habilitada.
- Mínimo 8 skills hardcodeadas para variedad.
- Presentación en grid responsive de tarjetas o lista detallada según ancho disponible.

3. **Acciones por skill**
- Cada skill incluye dropdown `⋮` con "Ver detalle" y "Eliminar".
- "Ver detalle" abre modal con descripción expandida, casos de uso y dependencias simuladas.
- Interacciones de modal/dropdown reutilizan comportamiento global común.

4. **Indicador cuantitativo de uso**
- El contador de adopción debe destacarse visualmente como número o badge.
- Debe ser fácil comparar skills muy usadas vs poco usadas.
- Soportar modo oscuro sin perder jerarquía visual.

## 3.5 Contrataciones de agentes

1. **Tabla de contratos activos y pasados**
- Columnas obligatorias: Cliente, Agente alquilado, Skills contratadas, Fechas contrato, Importe total, Acciones.
- Incluir registros de ejemplo activos y finalizados.
- Fechas en formato legible y consistente (por ejemplo `YYYY-MM-DD`).

2. **Representación de skills contratadas**
- En tabla, skills pueden mostrarse resumidas (chips + contador adicional si excede espacio).
- Debe evitar desbordes en móvil usando truncado controlado o layout apilado.
- En desktop, priorizar lectura horizontal sin scroll excesivo.

3. **Dropdown + modal de detalle de contrato**
- Dropdown por fila con al menos "Ver detalle".
- "Ver detalle" abre modal con desglose completo del contrato.
- El desglose incluye lista de skills con precio individual y total final claramente visible.

4. **Jerarquía financiera**
- El importe total debe destacarse en la tabla y repetirse en el modal.
- En el modal, subtotales y total deben diferenciarse tipográficamente.
- Debe existir claridad visual de cómo se compone el total pagado.

## 3.6 Log de errores

1. **Listado de errores de ejecución**
- Campos obligatorios: timestamp, agente, tipo de error, descripción breve, acciones.
- Mínimo 10 entradas hardcodeadas para simular histórico.
- Orden por recencia descendente (más reciente primero).

2. **Badges por tipo/gravedad**
- Tipos sugeridos: timeout, auth, parsing, integración, runtime.
- Cada tipo/gravedad se muestra con badge codificado por color.
- Además del color, incluir texto inequívoco para accesibilidad.

3. **Acciones por error**
- Dropdown `⋮` por entrada con "Ver detalle" y "Marcar como resuelto".
- "Ver detalle" abre modal con traza completa hardcodeada (stack trace multilinea).
- "Marcar como resuelto" actualiza estado visual de la fila (por ejemplo badge "resuelto").

4. **Manejo de legibilidad técnica**
- En el modal de traza usar tipografía monoespaciada y scroll interno.
- Mantener ancho/alto del modal controlado para no romper viewport móvil.
- El cierre debe funcionar con botón y backdrop.

## 4) Inventario de componentes reutilizables

1. **Sidebar persistente**
- Navegación entre las seis secciones.
- Estado activo visible por sección.

2. **Topbar con toggle de modo oscuro**
- Toggle global que agrega/quita clase `dark` en raíz.
- Debe afectar todas las secciones y componentes.

3. **Tarjeta de métrica**
- Componente reutilizable para KPI (icono, etiqueta, valor, acento).

4. **Dropdown de acciones (`⋮`)**
- Menú contextual reutilizable en tablas/listados.
- Cierre por click externo y exclusividad de menú abierto.

5. **Modal overlay**
- Reutilizable para detalles de usuario, agente, skill, contrato y error.
- Cierre por botón y click en backdrop.

6. **Badge semántico**
- Reutilizable para estados y severidades (usuario, agente, error).

7. **Lista de skills colapsable**
- Reutilizable en gestión de agentes y potencialmente contratos.
- Transición de expand/collapse suave.

8. **Tabla responsive base**
- Encabezados consistentes, filas legibles, fallback móvil apilado si aplica.

## 5) Criterios de aceptación (verificables)

1. Existe navegación lateral persistente con acceso visible a Dashboard, Gestión de usuarios, Gestión de agentes, Skills, Contrataciones de agentes y Log de errores.
2. El toggle de modo oscuro en topbar cambia toda la interfaz entre light/dark usando variantes `dark:` de Tailwind.
3. Dashboard muestra exactamente cuatro tarjetas KPI obligatorias con datos hardcodeados y un placeholder de actividad semanal debajo.
4. La sección de usuarios renderiza tabla con columnas Nombre, Email, Plan, Estado y Acciones.
5. El botón `⋮` en usuarios abre dropdown funcional con "Ver detalle" y "Eliminar".
6. Al accionar "Ver detalle" en usuarios se abre modal con datos extendidos; el modal se cierra con botón y backdrop.
7. La sección de agentes muestra nombre, propietario, estado y skills inicialmente ocultas por agente.
8. El control expandible de skills en agentes revela/oculta skills con transición suave.
9. El dropdown de agente incluye "Configurar" y abre modal con prompt de sistema; también incluye "Eliminar".
10. La sección de skills incluye texto explicativo sobre qué es una skill en AgentHub.
11. Cada skill muestra nombre, descripción y contador de agentes habilitados.
12. El dropdown por skill contiene "Ver detalle" y "Eliminar", y "Ver detalle" abre modal.
13. La sección de contrataciones muestra tabla con cliente, agente, skills, fechas, importe total y acciones.
14. El detalle de contrato en modal incluye desglose de skills con precios individuales y total final.
15. El log de errores muestra timestamp, agente, tipo, descripción y acciones.
16. Los errores usan badges codificados por tipo/gravedad y texto explícito legible.
17. "Ver detalle" de error abre modal con traza completa; "Marcar como resuelto" cambia estado visual del registro.
18. Todos los dropdowns cierran al hacer click fuera y solo permiten un menú abierto simultáneamente.
19. Todos los modales se superponen con backdrop, bloquean foco visual y cierran con botón + click en backdrop.
20. El prototipo mantiene usabilidad y legibilidad en viewport móvil y desktop.

## 6) Nota de proceso (Vision to spec)

Este documento es la fuente de verdad para implementar el prototipo HTML del panel de administración. Cualquier desarrollo visual posterior debe respetar estos requisitos antes de considerar variaciones estéticas.
