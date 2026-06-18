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

**2026-06-18** — Sesión opencode:
- **Horix Logistics**: Fix updater — ahora detecta automáticamente la rama actual del repo (master) en vez de hardcodear main, permitiendo actualizar desde la UI sin error.
- **Horix Logistics**: Nuevo modal de detalle de pedido — botón 👁️ en la tabla, muestra factura, cliente, dirección, ciudad, teléfono, valor, estado, ruta, coordenadas, fechas.
- **Horix Logistics**: Tabla `clientes` con migración — al importar SIESA se crean/actualizan clientes automáticamente, geocodificación para cada uno. Nueva página "Clientes" en el sidebar con buscador y lista.

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


