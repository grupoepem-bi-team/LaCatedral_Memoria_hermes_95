# 🏰 La Catedral — Mapa Vivo del Ecosistema Hermes .95

**Dashboard visual interactivo** que representa la infraestructura y automatizaciones del sistema Hermes .95 en tiempo real.

[![Deploy](https://img.shields.io/badge/deploy-Vercel-black?style=flat&logo=vercel)](https://vercel.com)
[![D3.js](https://img.shields.io/badge/D3.js-v7-F9A03C?style=flat&logo=d3.js)](https://d3js.org)
[![Python](https://img.shields.io/badge/Python-3.14+-3776AB?style=flat&logo=python)](https://python.org)

---

## 📖 Indice

- [Visión General](#visión-general)
- [Arquitectura del Sistema](#arquitectura-del-sistema)
- [Stack Tecnológico](#stack-tecnológico)
- [Generación Dinámica](#generación-dinámica)
- [Características Implementadas](#características-implementadas)
- [Deploy](#deploy)
- [Documentación Completa](#documentación-completa)
- [Autor](#autor)

---

## 🎯 Visión General

La Catedral es un **dashboard visual vivo** que mapea en tiempo real la infraestructura IT del ecosistema Hermes .95. Cada servidor es un pilar, cada componente una tarea orbital, y cada subtarea un detalle desplegable. Las conexiones entre servidores se representan como canales animados con partículas en movimiento.

**Metáfora visual:** Una catedral gótica donde los servidores son los pilares de piedra, los componentes orbitan como elementos decorativos, y los flujos de datos son canales de luz dorada.

### Inventario (v15.0-dynamic)

| Elemento | Cantidad |
|----------|----------|
| Servidores | 7 |
| Canales de datos | 9 |
| Componentes | 31 |
| Subtareas | 139 |
| Skills descubiertas | 97 |
| Scripts activos | 16 |
| Vaults de credenciales | 8 |
| Cron jobs | 2 |
| Indices tematicos | 5 |

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
| flow-6 | srv-95 | srv-99 | ssh | Health monitor cada 10 min |
| flow-7 | srv-95 | all | telegram | Alertas al grupo |
| flow-8 | srv-95 | github | deploy | Auto-deploy a Vercel |
| flow-9 | srv-95 | srv-99 | ssh | Logs Centralizado cada 5 min |

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
| Cron | Automatización cada 3 horas |
| Git + GitHub | Versionado y despliegue |

### Infraestructura

| Servicio | Propósito |
|----------|-----------|
| Vercel | Hosting estático con CDN global |
| Telegram Bot API | Alertas y notificaciones en tiempo real |
| SSH / WinRM / SMB | Conectividad a servidores heterogéneos |

---

## 🔄 Generación Dinámica

### Qué se escanea automáticamente

A diferencia de versiones anteriores (v14.0 y anteriores) que usaban datos **hardcodeados**, la v15.0 escanea el **filesystem real** en cada ejecución:

| Fuente | Ruta | Qué descubre |
|--------|------|-------------|
| Skills | `~/.hermes/skills/` | 97 skills en 16 categorías |
| Scripts | `~/.hermes/scripts/` | 16 scripts de automatización |
| Vault | `~/.hermes/vault/` | 8 vaults de credenciales |
| Logs Central | `~/logs-central/` | Recolección multi-protocolo |
| Cron Jobs | `crontab -l` | Tareas programadas |
| Indices | `~/.hermes/memory-deep/indices/` | 5 indices temáticos |
| Servidores | Ping ICMP | Estado online/offline |

### Frecuencia de actualización

| Configuración | Valor | Significado |
|---------------|-------|-------------|
| Schedule | `0 */3 * * *` | Cada 3 horas en punto |
| Horarios | 00:00, 03:00, 06:00, 09:00, 12:00, 15:00, 18:00, 21:00 | 8 veces por día |
| Máxima espera | 3 horas | Desde que creas algo hasta que se ve |
| Manual | Disponible | `cd ~/.hermes/memory-deep/scripts && python3 rebuild_dashboard.py` |

---

## ✨ Características Implementadas

### 🎨 Visualización

- **Layout radial con anti-colisión**: Algoritmo iterativo que resuelve solapamientos
- **Componentes orbitando**: Cada componente orbita su servidor padre con ángulo apuntando al centro
- **Canales animados**: Curvas Bézier con partículas que viajan por el trayecto
- **Glow effects**: Sombras difuminadas en canales y partículas
- **Metáfora catedral**: Fondo oscuro con gradientes dorados

### 🖱️ Interacción

| Acción | Comportamiento |
|--------|---------------|
| Click servidor | Centra + resalta servidor y conexiones (demás al 15%) |
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

---

## 🚀 Deploy

### Vercel (Auto-deploy)

El repositorio está conectado a Vercel. Cada push a `main` dispara re-deploy automático.

```bash
cd /tmp/LaCatedral
git add -A
git commit -m "auto: v15.0 dynamic"
git push origin main
```

### Ejecución Manual

```bash
# Generar HTML y data.json con datos reales del filesystem
python3 ~/.hermes/memory-deep/scripts/rebuild_dashboard.py

# Ver resultado local
firefox ~/.hermes/memory-deep/grafo/dashboard.html
```

---

## 📚 Documentación Completa

Para documentación técnica detallada (historial de versiones, solución de problemas, comandos útiles, arquitectura completa):

**[Leer DOCUMENTATION.md](DOCUMENTATION.md)**

Contenido del documento completo:
- Historial de cambios (v1.0 → v15.0)
- Configuración de cron jobs
- Solución de problemas comunes
- Comandos útiles para administración
- Descripción de cada skill, script y componente
- Flujos de datos detallados
- Parámetros de layout y anti-colisión

---

## 👤 Autor

**Emmanuel V.** — Equipo de Infraestructura y Automatización  
**Sistema:** Hermes .95 — Controlador central de memorias y monitoreo  
**Grupo:** EPEM BI Team

---

## 📄 Licencia

Proyecto interno. Uso exclusivo del equipo de infraestructura EPEM.

---

*"La Catedral no es un monumento estático. Es un organismo vivo que respira con cada skill, cada script, cada alerta."*
