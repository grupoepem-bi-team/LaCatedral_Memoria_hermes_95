# 📚 Documentacion Completa — La Catedral v15.0

## Fecha de documentacion: 2026-07-10
## Version actual: v15.0-dynamic
## Autor: Emmanuel V. / EPEM BI Team

---

## Tabla de Contenidos

1. [Que es La Catedral](#1-que-es-la-catedral)
2. [Arquitectura del Sistema](#2-arquitectura-del-sistema)
3. [Como funciona la actualizacion](#3-como-funciona-la-actualizacion)
4. [Que se escanea automaticamente](#4-que-se-escanea-automaticamente)
5. [Historial de cambios](#5-historial-de-cambios)
6. [Configuracion de cron jobs](#6-configuracion-de-cron-jobs)
7. [Solucion de problemas](#7-solucion-de-problemas)
8. [Comandos utiles](#8-comandos-utiles)

---

## 1. Que es La Catedral

La Catedral es un **dashboard visual vivo** que representa en tiempo real toda la infraestructura IT del ecosistema Hermes .95. Cada servidor es un pilar, cada componente orbita alrededor de su servidor, y los flujos de datos son canales animados con particulas en movimiento.

**Metafora visual:** Una catedral gotica donde los servidores son los pilares de piedra, los componentes orbitan como elementos decorativos, y los flujos de datos son canales de luz dorada.

### URL de acceso
- Repositorio: `https://github.com/grupoepem-bi-team/LaCatedral_Memoria_hermes_95`
- Despliegue: Vercel (auto-deploy en cada push)

---

## 2. Arquitectura del Sistema

### Servidores mapeados

| ID | Nombre | IP | Rol | Estado |
|----|--------|-----|-----|--------|
| srv-95 | HERMES .95 | localhost | Cerebro central | online |
| srv-250 | PROD .250 | 192.168.0.250 | MySQL 8.4 Master | unknown |
| srv-241 | ESPEJO .241 | 192.168.0.241 | Replica nativa | unknown |
| srv-240 | STAGING .240 | 192.168.0.240 | MySQL 5.7 Legacy | unknown |
| srv-99 | STAGING .99 | 192.168.0.99 | MySQL 8.4 Staging | unknown |
| srv-50 | BACKUP .50 | 192.168.0.50 | ZIPs de base de datos | unknown |
| srv-43 | RDP .43 | 192.168.0.43 | Escritorio remoto Windows | unknown |

### Inventario actual (v15.0)

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

### Canales de datos (Flows)

| ID | Origen | Destino | Tipo | Descripcion |
|----|--------|---------|------|-------------|
| flow-1 | srv-250 | srv-241 | replica | Replica MySQL nativa |
| flow-2 | srv-250 | srv-99 | restore | Restore pipeline nightly |
| flow-3 | srv-50 | srv-99 | backup | ZIP backup |
| flow-4 | srv-95 | srv-240 | ssh | Diagnostico remoto |
| flow-5 | srv-95 | srv-241 | ssh | Detector de drift |
| flow-6 | srv-95 | srv-99 | ssh | Health monitor cada 10 min |
| flow-7 | srv-95 | all | telegram | Alertas al grupo |
| flow-8 | srv-95 | github | deploy | Auto-deploy a Vercel |
| flow-9 | srv-95 | srv-99 | ssh | Logs Centralizado cada 5 min |

---

## 3. Como funciona la actualizacion

### Pipeline completo

```
PASO 1: Sincronizacion (nightly_sync.sh)
├── Escanear ~/.hermes/skills/         → Descubre skills
├── Escanear ~/.hermes/scripts/        → Descubre scripts
├── Escanear ~/.hermes/vault/          → Descubre credenciales
├── Escanear crontab                   → Descubre cron jobs
├── Escanear ~/logs-central/           → Verifica Logs Centralizado
├── Escanear ~/.hermes/memory-deep/indices/ → Descubre indices
├── Ping a servidores                  → Estado online/offline
└── Guardar en data.json

PASO 2: Rebuild (rebuild_dashboard.py)
├── Leer data.json                     → Datos actualizados
├── Calcular layout D3.js              → Posiciones anti-colisión
├── Generar dashboard.html             → HTML + JS inline + SVG
├── Generar data.json                  → Backup del estado
└── Push a GitHub                      → Auto-deploy Vercel

PASO 3: Despliegue (Vercel)
├── Detectar push a main             → Webhook
├── Rebuild estatico                  → CDN global
└── Dashboard disponible              → URL publica
```

### Frecuencia de actualizacion

| Periodo | Configuracion | Horarios (todos los dias) |
|---------|----------------|---------------------------|
| Cada 3 horas | `0 */3 * * *` | 00:00, 03:00, 06:00, 09:00, 12:00, 15:00, 18:00, 21:00 |

**Maximo tiempo de espera para ver cambios: 3 horas**

Si necesitas ver un cambio inmediatamente, ejecuta manualmente:
```bash
cd ~/.hermes/memory-deep/scripts && python3 rebuild_dashboard.py
```

---

## 4. Que se escanea automaticamente

### 4.1 Skills (~/.hermes/skills/)

El generador recorre recursivamente `~/.hermes/skills/` buscando archivos `SKILL.md`. Cada categoria (directorio de primer nivel) se convierte en un componente tipo "skill" bajo HERMES .95.

**Categorias descubiertas actualmente:**
- Apple (2 skills)
- Autonomous AI Agents (4 skills)
- Creative (15 skills)
- Data Science (1 skill)
- Devops (20 skills)
- Email (1 skill)
- General (1 skill)
- Github (6 skills)
- Media (4 skills)
- Mlops (8 skills)
- Note Taking (1 skill)
- Productivity (10 skills)
- Research (6 skills)
- Smart Home (1 skill)
- Social Media (1 skill)
- Software Development (9 skills)

### 4.2 Scripts (~/.hermes/scripts/)

Todos los archivos ejecutables en `~/.hermes/scripts/` se descubren dinamicamente y se agrupan en el componente "Scripts del Sistema".

**Scripts detectados:**
- verificar-y-archivar-diario.sh
- recolectar-logs-central.sh
- rebuild_dashboard.sh
- nightly_sync.sh
- detector_datos_desactualizados_espejo.py
- verificar-backup-50.sh
- monitor-restore-99-v5.py
- monitor-restore-99-v4.py
- monitor-restore-99-v3.py
- monitor-restore-99-v2.py
- playbook-99-diario.sh
- formato-reporte.sh
- monitor-restore-99.py
- playbook-99-analisis.sh
- check_and_sync.py
- Y mas...

### 4.3 Logs Centralizado (~/logs-central/)

Si existe el directorio `~/logs-central/`, se crea automaticamente el componente "Logs Centralizado" con subtareas para cada protocolo de recoleccion.

**Servidores monitoreados:**
- .250, .241, .240 (via SSH)
- .43 (via WinRM)
- .50 (via SMB)

### 4.4 Vault de Credenciales (~/.hermes/vault/)

Cada archivo `.json` en `~/.hermes/vault/` se convierte en una subtarea del componente "Vault de Credenciales".

**Vaults activos:**
- windows_43.json
- smb_backup_db.json
- mysql_espejo.json
- telegram_staging99.json
- mysql_espejo_escritura.json
- mysql_espejo_root.json
- mysql_espejo_analistas.json
- ssh_192.168.0.241.json

### 4.5 Cron Jobs (crontab)

El crontab del usuario se lee automaticamente y cada linea activa se convierte en una subtarea del componente "Cron Jobs".

### 4.6 Deep Memory System

El componente "Deep Memory System" muestra los scripts internos del sistema de memorias profundas:
- auto_tag.py
- persist_memory.py
- search_deep.py
- manage_procedure.py

### 4.7 Indices Tematicos (~/.hermes/memory-deep/indices/)

Cada subdirectorio en `indices/` se convierte en una subtarea del componente "Indices Tematicos".

---

## 5. Historial de cambios

### v1.0 - v5.0: Fundamentos
- **v1.0**: Estructura de directorios y base de datos SQLite
- **v2.0**: Script auto_tag.py para categorizacion jerarquica
- **v3.0**: Layout radial basico con D3.js
- **v4.0**: Metafora gotica (arcos, vitrales, boveda de cruceria)
- **v5.0**: Integracion Tailwind CSS + Google Fonts

### v5.1 - v7.0: Estabilidad
- **v5.1**: Fix de f-strings anidados que truncaban JSON
- **v6.0**: Mapeo de arquitectura real (7 servidores, 8 canales, 6 componentes)
- **v7.0**: Sistema de categorias jerarquico con 128 items y 81 skills

### v8.0 - v8.4: Experiencia Humana
- **v8.0**: Cards explicativas con iconos + canales animados
- **v8.1**: Tercer nivel jerarquico (subtareas desplegables) — 30 subtareas
- **v8.2**: Componentes orbitan fisicamente su servidor padre
- **v8.3**: Distribucion real de tareas por nodo (48 subtareas)
- **v8.4**: Subtareas en grafo (badge dorado + mini-nodos)

### v9.0 - v10.0: Layout Espacioso + Navegacion
- **v9.0**: Layout espacioso sin mini-nodos encimados, detail panel deslizable
- **v9.1**: Resumen humano obligatorio en cada subtarea
- **v10.0**: Navegacion inteligente (click nodo → zoom centrado)

### v11.0 - v12.0: Features Completas
- **v11.0**: Buscador global (Ctrl+K), barras de progreso, filtros
- **v11.0**: Estados en tiempo real (ping cada 50s)
- **v11.0**: Exportar JSON, auto-refresh
- **v12.0**: Responsive design completo
- **v12.1**: Zero superposicion (padding aumentado)

### v14.0 - v14.2: JS Inline Robusto + Canales Visibles
- **v14.0**: JS inline sin f-strings anidados
- **v14.0**: Event delegation (elimina onclick inline)
- **v14.1**: Fix variable `cy`, distribucion angular apuntando al centro
- **v14.2**: Canales mas visibles (2.8x opacidad), glow effects

### v15.0: Generacion Dinamica (CAMBIO MAYOR)
- **v15.0**: `collect_real_data()` reescrito para escanear filesystem real
- **v15.0**: 97 skills descubiertas dinamicamente (antes 0)
- **v15.0**: 16 scripts descubiertos dinamicamente (antes 0)
- **v15.0**: Vault, Logs Central, Cron Jobs, Indices descubiertos
- **v15.0**: Componentes: 13 → 31 (+18 nuevos)
- **v15.0**: Subtareas: 48 → 139 (+91 nuevas)
- **v15.0**: Frecuencia actualizada a cada 3 horas (antes 1 vez por dia)

---

## 6. Configuracion de cron jobs

### Jobs activos relacionados con La Catedral

| Nombre | Job ID | Horario | Script | Estado |
|--------|--------|---------|--------|--------|
| Sync + Rebuild | 062df754a68a | 0 */3 * * * | nightly_sync.sh | ✅ Activo |
| Rebuild + Push | de4b369f40f1 | 0 */3 * * * | rebuild_dashboard.sh | ✅ Activo |

### Jobs del ecosistema (no relacionados directamente)

| Nombre | Horario | Funcion |
|--------|---------|---------|
| monitor-restore-99-tablas | */10 * * * * | Monitorea restore .99 cada 10 min |
| detector-drift-espejo | 0 9 * * * | Detecta drift .250 vs .241 a las 9 AM |
| recolectar-logs-central | */5 * * * * | Recolecta logs cada 5 min |
| verificar-logs-central-diario | 0 9 * * * | Verifica logs central cada manana |
| verificar-backup-50-manana | 0 5-8 * * * | Verifica backup .50 de 5 a 8 AM |

---

## 7. Solucion de problemas

### Problema: "No veo mis cambios en La Catedral"

**Causa probable:** El ultimo rebuild fue hace menos de 3 horas.

**Soluciones:**
1. Esperar a la proxima ventana de 3 horas (00:00, 03:00, 06:00, etc.)
2. Ejecutar manualmente:
   ```bash
   cd ~/.hermes/memory-deep/scripts && python3 rebuild_dashboard.py
   ```

### Problema: "SyntaxError en el navegador"

**Causa probable:** Comillas simples escapadas mal en JS inline.

**Estado:** Corregido en v14.0 con event delegation (sin onclick inline).

### Problema: "Los nodos se superponen"

**Causa probable:** Muchos componentes en un mismo servidor.

**Solucion:** El layout usa algoritmo anti-colisión con padding de 40px y orbitas condicionales (160px centro, 150px bordes).

**Verificacion:** Abrir consola del navegador y ejecutar:
```javascript
(function checkOverlap(){ var nodes=[]; document.querySelectorAll('.server-node').forEach(function(g){ var m=g.getAttribute('transform').match(/translate\(([^,]+),([^)]+)\)/); if(m) nodes.push({x:parseFloat(m[1]),y:parseFloat(m[2]),r:65}); }); document.querySelectorAll('.comp-node').forEach(function(g){ var m=g.getAttribute('transform').match(/translate\(([^,]+),([^)]+)\)/); if(m) nodes.push({x:parseFloat(m[1]),y:parseFloat(m[2]),r:32}); }); var overlaps=0; for(var i=0;i<nodes.length;i++) for(var j=i+1;j<nodes.length;j++){ var a=nodes[i],b=nodes[j]; var dx=b.x-a.x,dy=b.y-a.y; var dist=Math.sqrt(dx*dx+dy*dy); if(dist<a.r+b.r+40&&dist>0) overlaps++; } return 'Nodos: '+nodes.length+', Superposiciones: '+overlaps; })()
```

### Problema: "El SVG aparece vacio"

**Causa probable:** Viewport headless con clientWidth=0.

**Solucion:** Usa viewBox fijo 1400x800 con zoomToFit() al cargar.

---

## 8. Comandos utiles

### Regenerar manualmente
```bash
cd ~/.hermes/memory-deep/scripts && python3 rebuild_dashboard.py
```

### Verificar data.json
```bash
cat ~/.hermes/memory-deep/grafo/data.json | python3 -m json.tool | head -50
```

### Ver logs de ejecucion
```bash
cat ~/.hermes/memory-deep/logs/rebuild_dashboard.log
cat ~/.hermes/memory-deep/logs/nightly_sync.log
```

### Ver estado de cron jobs
```bash
hermes cron list
```

### Ver skills en disco
```bash
find ~/.hermes/skills -name "SKILL.md" | wc -l
```

### Ver scripts en disco
```bash
ls ~/.hermes/scripts/ | wc -l
```

### Verificar superposiciones en el dashboard
Abrir consola del navegador (F12) → Pegar el codigo del Problema 3.

---

## Archivos clave

| Archivo | Proposito |
|---------|-----------|
| `~/.hermes/memory-deep/scripts/rebuild_dashboard.py` | Generador principal del HTML |
| `~/.hermes/memory-deep/scripts/nightly_sync.sh` | Sincronizacion de datos |
| `~/.hermes/memory-deep/grafo/dashboard.html` | Dashboard generado (subir a GitHub) |
| `~/.hermes/memory-deep/grafo/data.json` | Datos extraidos del sistema |
| `~/.hermes/memory-deep/db/memory.db` | SQLite con memorias |
| `~/.hermes/memory-deep/sql/schema.sql` | Schema de la base de datos |
| `/tmp/LaCatedral/` | Repo GitHub local |

---

## Contacto

**Emmanuel V.** — Equipo de Infraestructura y Automatizacion
**Sistema:** Hermes .95
**Grupo:** EPEM BI Team

---

*"La Catedral no es un monumento estatico. Es un organismo vivo que respira con cada skill, cada script, cada alerta."*
