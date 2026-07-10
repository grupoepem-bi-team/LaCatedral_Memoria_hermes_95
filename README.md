# 🏰 La Catedral — Mapa Vivo del Ecosistema Hermes .95

**Dashboard visual interactivo** que representa la infraestructura y automatizaciones del sistema Hermes .95 en tiempo real.

[![Deploy](https://img.shields.io/badge/deploy-Vercel-black?style=flat&logo=vercel)](https://vercel.com)
[![D3.js](https://img.shields.io/badge/D3.js-v7-F9A03C?style=flat&logo=d3.js)](https://d3js.org)
[![Python](https://img.shields.io/badge/Python-3.14+-3776AB?style=flat&logo=python)](https://python.org)

---

## 📖 Índice

- [Visión General](#visión-general)
- [Arquitectura del Sistema](#arquitectura-del-sistema)
- [Stack Tecnológico](#stack-tecnológico)
- [Estructura de Datos](#estructura-de-datos)
- [Características Implementadas](#características-implementadas)
- [Generador de Dashboard](#generador-de-dashboard)
- [Historial de Desarrollo](#historial-de-desarrollo)
- [Deploy](#deploy)
- [Autor](#autor)

---

## 🎯 Visión General

La Catedral es un **dashboard visual vivo** que mapea en tiempo real la infraestructura IT del ecosistema Hermes .95. Cada servidor es un pilar, cada componente una tarea orbital, y cada subtarea un detalle desplegable. Las conexiones entre servidores se representan como canales animados con partículas en movimiento.

**Metafora visual:** Una catedral gótica donde los servidores son los pilares de piedra, los componentes orbitan como elementos decorativos, y los flujos de datos son canales de luz dorada.

### Inventario

| Elemento | Cantidad |
|----------|----------|
| Servidores | 7 |
| Canales de datos | 8 |
| Componentes | 13 |
| Subtareas | 48 |
| Estadísticas | 27 done, 15 active, 6 pending |

---

## 🏗️ Arquitectura del Sistema

### Servidores Mapeados

| ID | Nombre | IP | Rol | Estado |
|----|--------|-----|-----|--------|
| srv-95 | HERMES .95 | localhost | Cerebro (controlador) | online |
| srv-250 | PROD .250 | 192.168.0.250 | MySQL 8.4 Master | unknown |
| srv-241 | ESPEJO .241 | 192.168.0.241 | Replica nativa | unknown |
| srv-240 | STAGING .240 | 192.168.0.240 | MySQL 5.7 Legacy | unknown |
| srv-99 | STAGING .99 | 192.168.0.99 | MySQL 8.4 Staging | unknown |
| srv-50 | BACKUP .50 | 192.168.0.50 | ZIPs de base de datos | unknown |
| srv-43 | RDP .43 | 192.168.0.43 | Escritorio remoto | unknown |

### Canales de Datos (Flows)

| ID | Origen | Destino | Tipo | Descripción |
|----|--------|---------|------|-------------|
| flow-1 | srv-250 | srv-241 | replica | Replica MySQL nativa |
| flow-2 | srv-250 | srv-99 | restore | Restore pipeline nightly |
| flow-3 | srv-50 | srv-99 | backup | ZIP backup |
| flow-4 | srv-95 | srv-240 | ssh | Diagnóstico remoto |
| flow-5 | srv-95 | srv-241 | ssh | Detector de drift |
| flow-6 | srv-95 | srv-99 | ssh | Health monitor |
| flow-7 | srv-95 | all | telegram | Alertas al grupo |
| flow-8 | srv-95 | github | deploy | Auto-deploy a Vercel |

### Componentes por Servidor

| Servidor | Componentes | Subtareas |
|----------|-------------|-----------|
| HERMES .95 | Sync Nocturno, Rebuild Dashboard, Alertas Telegram | 16 |
| PROD .250 | MySQL 8.4 Master, Replicación | 7 |
| ESPEJO .241 | MySQL Replica, Detector Drift | 7 |
| STAGING .240 | MySQL 5.7 | 2 |
| STAGING .99 | Restore Pipeline, Monitor Health | 7 |
| BACKUP .50 | ZIP Backup | 4 |
| RDP .43 | Servicio RDP, Recordatorio | 5 |

---

## 🛠️ Stack Tecnológico

### Frontend

| Tecnología | Versión | Propósito |
|------------|---------|-----------|
| D3.js | v7 | Motor de visualización SVG, zoom, pan, layout |
| Vanilla JS | ES5 | Lógica de interacción (compatibilidad máxima) |
| CSS3 | Custom | Animaciones, responsive design, glassmorphism |
| SVG | Native | Renderizado vectorial de nodos y conexiones |

### Backend / Generador

| Tecnología | Propósito |
|------------|-----------|
| Python 3.14+ | Script generador de HTML estático |
| SQLite + FTS5 | Base de datos de memorias del sistema |
| Cron | Automatización de sync nocturno |
| Git + GitHub | Versionado y despliegue |

### Infraestructura

| Servicio | Propósito |
|----------|-----------|
| Vercel | Hosting estático con CDN global |
| Telegram Bot API | Alertas y notificaciones en tiempo real |
| SSH / WinRM / SMB | Conectividad a servidores heterogéneos |

---

## 📊 Estructura de Datos

El sistema consume un archivo `data.json` generado dinámicamente:

```json
{
  "meta": {
    "generated_at": "2026-07-10T16:26:32",
    "version": "14.2"
  },
  "servers": [...],
  "flows": [...],
  "components": [
    {
      "id": "comp-95-1",
      "name": "Sync Nocturno",
      "type": "cron",
      "server": "srv-95",
      "status": "active",
      "schedule": "3:00 AM",
      "human_desc": "Limpia memorias y recalcula VIP.",
      "last_run": "03:00",
      "icon": "🌙",
      "subtasks": [
        {
          "name": "Cargar MEMORY.md",
          "desc": "Lee archivo",
          "status": "done",
          "icon": "📂",
          "human_summary": "Abre el archivo donde guardamos todo lo aprendido."
        }
      ]
    }
  ]
}
```

Cada subtarea incluye obligatoriamente:
- `name`: Nombre técnico
- `desc`: Descripción corta
- `status`: `done` | `active` | `pending`
- `icon`: Emoji representativo
- `human_summary`: Explicación en lenguaje natural para no técnicos

---

## ✨ Características Implementadas

### 🎨 Visualización

- **Layout radial con anti-colisión**: Algoritmo iterativo que resuelve solapamientos entre nodos
- **Componentes orbitando**: Cada componente orbita su servidor padre con ángulo apuntando al centro
- **Canales animados**: Curvas Bézier con partículas que viajan por el trayecto
- **Glow effects**: Sombras difuminadas en canales y partículas
- **Metáfora catedral**: Fondo oscuro con arcos, gradientes dorados, pilares laterales

### 🖱️ Interacción

| Acción | Comportamiento |
|--------|---------------|
| Click servidor | Centra + resalta servidor y sus conexiones (demás al 15% opacidad) |
| Click componente | Abre panel de detalle con subtareas expandibles |
| Click fondo | ZoomToFit a vista general, restaura opacidad |
| Hover nodo | Tooltip con descripción + preview de subtareas |
| Ctrl+K | Overlay de búsqueda global |
| Escape | Cierra todo, vuelve a vista general |

### 📱 Responsive Design

| Breakpoint | Layout |
|------------|--------|
| < 380px | Header compacto, drawer lateral, nodos reducidos |
| 380-767px | Drawer para panel lateral, bottom sheet para detalle |
| 768-1199px | Panel lateral fijo (340px), detail panel flotante |
| ≥ 1200px | Panel lateral ancho (400px), detail panel ancho (340px) |

### 📊 Panel Lateral

- Agrupado por servidor con headers colapsables
- Cards de componente con barra de progreso
- Event delegation para clicks (sin onclick inline)

### 🔍 Búsqueda Global

- Indexado en runtime: servidores + componentes + subtareas
- Resultados limitados a 10
- Navegación directa al nodo al hacer click

### 📥 Exportación

- Botón "📥 JSON" descarga `la_catedral_estado_YYYY-MM-DD.json`
- Incluye datos completos + info de exportación

---

## 🔧 Generador de Dashboard

### `rebuild_dashboard.py`

Script Python que:

1. **Recolecta datos reales** del sistema (ping a servidores, skills, crontab)
2. **Calcula layout** con algoritmo anti-colisión
3. **Genera HTML estático** con JS inline y JSON embebido
4. **Pushea a GitHub** para auto-deploy en Vercel

### Parámetros de Layout

```javascript
var W = 1400, H = 800;           // ViewBox SVG
var SRV_R_OUTER = 65;            // Radio servidor externo
var SRV_R_INNER = 50;            // Radio servidor interno
var COMP_R = 32;                 // Radio componente
var PAD = 40;                    // Padding entre nodos
var R = 440;                     // Radio del círculo de servidores
var orbitR_center = 160;         // Órbita componentes del centro
var orbitR_border = 150;         // Órbita componentes del borde
```

### Algoritmo Anti-Colisión

```
1. Posicionar servidores en círculo de radio R (srv-95 en centro)
2. Calcular ángulo de componentes apuntando al centro del viewBox
3. Clamp de coordenadas dentro del viewBox con margen
4. Resolver colisiones iterativamente (máx 100 iteraciones)
5. Empujar nodos solapados con fuerza proporcional al overlap
```

---

## 📜 Historial de Desarrollo

### v1.0 - v5.0: Fundamentos
- **v1.0**: Estructura de directorios y base de datos SQLite
- **v2.0**: Script `auto_tag.py` para categorización jerárquica
- **v3.0**: Layout radial básico con D3.js
- **v4.0**: Metáfora gótica (arcos, vitrales, bóveda de crucería)
- **v5.0**: Integración Tailwind CSS + Google Fonts (Cinzel, MedievalSharp)

### v5.1 - v7.0: Estabilidad
- **v5.1**: Fix de f-strings anidados que truncaban JSON
- **v6.0**: Mapeo de arquitectura real (7 servidores, 8 canales, 6 componentes)
- **v7.0**: Sistema de categorías jerárquico con 128 items y 81 skills

### v8.0 - v8.4: Experiencia Humana
- **v8.0**: Cards explicativas con iconos + canales animados con partículas
- **v8.1**: Tercer nivel jerárquico (subtareas desplegables) — 30 subtareas
- **v8.2**: Componentes orbitan físicamente su servidor padre
- **v8.3**: Distribución real de tareas por nodo (48 subtareas totales)
- **v8.4**: Subtareas en grafo (badge dorado + mini-nodos expandibles)

### v9.0 - v10.0: Layout Espacioso + Navegación
- **v9.0**: Layout espacioso sin mini-nodos encimados, detail panel deslizable
- **v9.1**: Resumen humano obligatorio en cada subtarea
- **v10.0**: Navegación inteligente (click nodo → zoom centrado + resalta conexiones)

### v11.0 - v12.0: Features Completas
- **v11.0**: Buscador global (Ctrl+K), barras de progreso, filtros por estado
- **v11.0**: Estados en tiempo real (ping cada 50s), mini-leyenda, stats globales
- **v11.0**: Exportar JSON, auto-refresh página cada 5 min
- **v12.0**: Responsive design completo (mobile/tablet/desktop)
- **v12.1**: Zero superposición (padding aumentado + órbita condicional)

### v13.0: Separación JSON
- **v13.0**: Separación de datos JSON del código JS para evitar truncamiento

### v14.0 - v14.2: JS Inline Robusto + Canales Visibles
- **v14.0**: JS inline escrito completamente sin f-strings anidados
- **v14.0**: Event delegation para eliminar onclick inline con comillas escapadas
- **v14.1**: Fix de variable `cy` faltante, distribución angular apuntando al centro
- **v14.2**: Canales más visibles (2.8x opacidad), glow effects, partículas más grandes, labels más legibles

---

## 🚀 Deploy

### Vercel (Auto-deploy)

El repositorio está conectado a Vercel. Cada push a `main` dispara re-deploy automático.

```bash
cd /tmp/LaCatedral
git add -A
git commit -m "auto: v14.2 Canales visibles"
git push origin main
```

### Ejecución Manual

```bash
# Generar HTML y data.json
python3 ~/.hermes/memory-deep/scripts/rebuild_dashboard.py

# Ver resultado local
firefox ~/.hermes/memory-deep/grafo/dashboard.html
```

### Automatización (Cron)

```bash
# Sync nocturno a las 3:00 AM
0 3 * * * /home/vm-hermes/.hermes/memory-deep/scripts/nightly_sync.sh

# Rebuild dashboard a las 3:05 AM
5 3 * * * /home/vm-hermes/.hermes/memory-deep/scripts/rebuild_dashboard.sh
```

---

## 👤 Autor

**Emmanuel V.** — Equipo de Infraestructura y Automatización  
**Sistema:** Hermes .95 — Controlador central de memorias y monitoreo  
**Grupo:** EPEM BI Team

---

## 📄 Licencia

Proyecto interno. Uso exclusivo del equipo de infraestructura EPEM.

---

*"La Catedral no es un monumento estático. Es un organismo vivo que respira con cada ping, cada sync, cada alerta."*
