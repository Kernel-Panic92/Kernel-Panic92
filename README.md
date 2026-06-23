## Hola soy Edgar Velásquez

**Ingeniero de software** construyendo sistemas modulares, escalables y sostenibles.

---

### 🚧 Proyecto actual: Horix Platform

Plataforma ERP con módulos independientes (cada uno con su propia auth y frontend) y un **Launcher** que orquesta todo: CRUD de módulos, health checks, generación de nginx y **MCP Gateway** unificado.

```
           Nginx SSL
         ┌────┴────┐
         │         │
    Launcher   MCP Gateway
    (SPA)      ── sessiones x módulo
    ├── Users  ── OAuth DCR (opcional)
    ├── Nginx  ── 16 tools Horix
    ├── SMTP   ── 13 tools DocFlow
    └── MCP URL
         │
    ┌────┴────┐
    │         │
  Horix     DocFlow
  (HR,      (Facturas,
   Payroll)  Proveedores)
```

**Stack:** Node.js, Express, SQLite, PostgreSQL, JWT, Nginx, PM2  
**Principios:** Módulos autónomos, sin acoplamiento, cada módulo gestiona su propio auth

### 📋 Bitácora

**2026-06-23** — Sesión opencode:
- **horix-erp (framework)**: Creado `framework/README.md` con guía completa para crear módulos (backend, MCP, registro, nginx, PM2). Soporte `basePath` en initHorixFramework para proxy prefix.
- **horix-erp (docs)**: Documentado estado actual del servidor (puertos, nginx, PM2, accesos) en AGENTS.md y README.md. Agregada Clean Install Guide para servidor nuevo (puerto único 443 + path prefix).
- **Horix Logistics (MCP)**: Protocolo JSON-RPC 2.0 completo con 9 tools ejecutables contra DB.
- **Horix Logistics (HTTPS)**: Registrado en la plataforma como módulo `/logistics/`. Health check agregado (`GET /health`). Accesible vía `:9443/logistics/`.
- **Horix Logistics (BASE path)**: Fix session loss en hard refresh — auto-detección de `BASE` desde `location.pathname` para API calls detrás de proxy prefix. Fix function `logout()` faltante.
- **Logistics**: Agregado AGENTS.md con contexto del proyecto.

**2026-06-19** — Sesión opencode:
- **Horix Logistics**: Fix `s.latitud.toFixed is not a function` — PostgreSQL DECIMAL devuelve strings, se usa `Number()` en frontend para convertir antes de `toFixed()`.
- **Horix Logistics**: Fix `vehiculosUsar` duplicado en `vrp.js` — error de sintaxis que impedía iniciar el servicio tras actualización.
- **Horix Logistics**: Fix query pedidos en `rutas.js` — retornaba `latitud/longitud` pero VRP esperaba `lat/lng`, se agregó alias SQL.
- **Horix Logistics**: Mapa en modal de pedido + Google Places Autocomplete actualiza marcador en mapa.
- **Horix Logistics**: Selector de sede y vehículo filtrado por sede en modal de pedido + campos lat/lng en tabla.
- **Horix Logistics**: Fix `actualizarMapaPin` para detectar correctamente el mapa de pedido (`p-lat/p-lng`).
- **Horix Logistics**: CRUD completo de rutas con bulk delete (individual y masivo), endpoint debug `/api/rutas/diagnostico` sin auth.
- **Pendiente**: Al generar rutas, el vehículo del pedido no se usa — VRP asigna round-robin ignorando `vehiculo_id`.

**2026-06-18** — Sesión opencode (4ª parte):
- **DocFlow + Horix**: Replicado el layout de SMTP de Logistics (card con `max-width:600px`) en ambos módulos. DocFlow ahora usa la misma card sencilla. Horix cambió de grid 2-columnas a 2 cards apiladas verticalmente (SMTP + Plantilla de Correo), eliminando el problema de espacios desiguales al maximizar.
- **Launcher**: Nuevo endpoint `GET /api/smtp/internal` sin auth para que los módulos hereden la configuración SMTP.
- **Horix Logistics**: Implementada herencia SMTP desde el Launcher — flag `smtp_heredar` + `launcher_url` en config, email.js y test SMTP usan fetch al launcher cuando `smtp_heredar = true`. Frontend: checkbox "Heredar del Launcher" desactiva campos SMTP locales y muestra URL del Launcher.
- **Horix**: Misma herencia SMTP implementada en backend (email.js con fetch al launcher) y frontend (checkbox en pestaña Correo).
- **DocFlow**: Misma herencia SMTP implementada en backend (smtp.service.js con fetch al launcher al obtener config) y frontend (checkbox + test con inherit=1).
- **horix-erp**: Creado `framework/` con base.css, components.css, framework.js, theme.js, init.sh + endpoint `/api/shell/config` para que nuevos módulos (CRM, etc.) hereden la UI estandarizada sin depender del launcher en runtime.

**2026-06-18** — Sesión opencode (2ª parte):
- **Horix Logistics**: Card grid para clientes con avatar+iniciales, selección múltiple, pg_trgm fuzzy matching, búsqueda.
- **Horix Logistics**: SIESA parser reescrito — formato 3 líneas (nombre / dos valores+FEV / ciudad+dir+tel), captura valor_contado+valor_credito, conductor, placa, nro_guia.
- **Horix Logistics**: Nuevos campos en pedidos (valor_contado, conductor, placa, nro_guia) + migración 009.
- **Horix Logistics**: Auto-creación de vehículo al importar SIESA si la placa no existe.
- **Horix Logistics**: Google Places Autocomplete en formulario cliente + pestaña Mapas en Config para API key.
- **Horix Logistics**: Buscador y filtro por estado en Pedidos y Vehículos.
- **Horix Logistics**: Fix thousand separators — pg devuelve NUMERIC como string, se envuelve con Number() para que toLocaleString() funcione.

**2026-06-18** — Sesión opencode:
- **Horix Logistics**: Fix updater — ahora detecta automáticamente la rama actual del repo (master) en vez de hardcodear main, permitiendo actualizar desde la UI sin error.
- **Horix Logistics**: Nuevo modal de detalle de pedido — botón 👁️ en la tabla, muestra factura, cliente, dirección, ciudad, teléfono, valor, estado, ruta, coordenadas, fechas.
- **Horix Logistics**: Tabla `clientes` con migración — al importar SIESA se crean/actualizan clientes automáticamente, geocodificación para cada uno. Nueva página "Clientes" en el sidebar con buscador y lista.
- **Horix Logistics**: CRUD completo para Vehículos, Pedidos y Clientes — botones ✏️ 🗑️ en tablas, modales de creación/edición, confirmación de eliminación.
- **Horix Logistics**: Parser SIESA reforzado — 4 estrategias de detección de filas FEV, división flexible de columnas, fallbacks múltiples.
- **Horix Logistics**: Bulk delete con checkboxes para Vehículos, Pedidos y Clientes — selección múltiple, botón "Eliminar", endpoint backend por lotes.

**2026-06-17** — Sesión opencode (2ª parte):
- **Horix Logistics**: Fix parser SIESA — ahora con detección flexible de tabla, fallback para facturas sin prefijo FEV-, y debug visual en frontend para diagnosticar cuando no se extraen pedidos.

**2026-06-17** — Sesión opencode:
- **Horix Logistics**: Nuevo módulo **Actualizador** completo — backend con endpoints status/check/update/restart/logs + pestaña en Configuración con versión, verificación y actualización one-click desde la UI.
- **Horix Logistics**: Fix en importación de archivos — drop zones ahora soportan arrastrar y soltar, feedback visual cuando se hace clic en importar sin archivo seleccionado.
- **Horix Logistics**: Creados `AGENTS.md` y `BITACORA.md` en el repo (movidos después a `horix-erp/AGENTS.md` y este README).

**2026-06-16** — Sesión opencode (2ª parte):
- **horix-erp (launcher)**: Nueva pestaña **Respaldo** con exportación/importación de configuración (módulos, config, usuarios) vía JSON. Útil para reinstalaciones.
- **horix-erp (launcher)**: Dashboard principal ahora muestra borde verde/amarillo/rojo en tarjetas de módulos según estado MCP.
- **horix-erp (launcher)**: Versión `v1.0.0` release creada + versión visible junto al nombre de usuario.
- **Horix**: Endpoint `/api/version` agregado para mostrar versión desde package.json en el sidebar.
- **DocFlow**: Fix en `api.js` — ahora redirige al login cuando el servidor responde 401 (sesión expirada).
- **horix-erp (launcher)**: Widget **Servidor** en dashboard (solo admin) con CPU, RAM, disco, hostname, uptime.

**2026-06-16** — Sesión opencode:
- **horix-erp (launcher)**: Fix health check para que caiga a `/mcp` cuando `/health` responde no-OK (404). Fix PM2 name mapping `wordpress → wordpress-mcp` para status y reinicio. Fix trailing slash en URLs de módulos.
- **Horix**: Updater cambia a `sudo pm2 restart horix` (corre bajo root). Agregado tab **Telemetría** en configuración (frontend + script tag en index.html).
- **Servidor Docker**: Horix migrado a PM2 de root con `sudo pm2 start`.

### Últimas features
- **MCP Gateway** unificado con OAuth 2.0 DCR + Authorization Code flow (compatible con Claude Desktop/Web)
- **Password recovery** vía SMTP configurable desde Admin
- **Nginx generator** desde la UI con prefixes por módulo
- **DocFlow MCP**: 13 tools (facturas, dashboard, eventos, vencimientos DIAN) → ahora con tools `causar_factura` y `pagar_factura`, transacciones ACID, queries parametrizadas y registro de auditoría
- **Horix MCP**: 16 tools (registros, empleados, reportes, exportación CSV)
- **Horix Config UI** rediseñada con layout de tabs tipo DocFlow (Correo, Backup, Seguridad, Auditoría, Permisos, Actualizar) y **updater** desde la interfaz vía `git pull + npm install + pm2 restart`
- **Launcher updater**: tab "Actualizar" en el admin del orquestador con `git fetch + reset hard + npm install` y reinicio automático vía PM2
- **Responsive design** para mobile
- **Windows TLS fix** para firewalls corporativos (FortiGate)

▶️ [Roadmap](https://github.com/Kernel-Panic92/horix-erp/blob/main/ROADMAP.md) · [Repositorio](https://github.com/Kernel-Panic92/horix-erp)

---

### 🧰 Tecnologías

`JavaScript` · `Node.js` · `Express` · `PostgreSQL` · `SQLite` · `Nginx` · `Git` · `PM2` · `MCP`

---

### 📫 Contacto

[GitHub](https://github.com/Kernel-Panic92)


