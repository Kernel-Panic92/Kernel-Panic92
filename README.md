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

### Últimas features
- **MCP Gateway** unificado con OAuth 2.0 DCR + Authorization Code flow (compatible con Claude Desktop/Web)
- **Password recovery** vía SMTP configurable desde Admin
- **Nginx generator** desde la UI con prefixes por módulo
- **DocFlow MCP**: 13 tools (facturas, dashboard, eventos, vencimientos DIAN)
- **Horix MCP**: 16 tools (registros, empleados, reportes, exportación CSV)
- **Responsive design** para mobile
- **Windows TLS fix** para firewalls corporativos (FortiGate)

▶️ [Roadmap](https://github.com/Kernel-Panic92/horix-erp/blob/main/ROADMAP.md) · [Repositorio](https://github.com/Kernel-Panic92/horix-erp)

---

### 🧰 Tecnologías

`JavaScript` · `Node.js` · `Express` · `PostgreSQL` · `SQLite` · `Nginx` · `Git` · `PM2` · `MCP`

---

### 📫 Contacto

[GitHub](https://github.com/Kernel-Panic92)
