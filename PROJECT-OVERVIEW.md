# 🚀 DevLake Demo - Banco Columbia
## Repositorio Completo y Listo para Deployment

```
    ____             _           _         
   |  _ \  _____   _| |     __ _| | _____  
   | | | |/ _ \ \ / / |    / _` | |/ / _ \ 
   | |_| |  __/\ V /| |___| (_| |   <  __/ 
   |____/ \___| \_/ |_____|\__,_|_|\_\___| 
                                            
   Banco Columbia - Production Ready Demo
```

---

## 📦 Contenido del Repositorio

### 📄 Documentación Principal

| Archivo | Descripción | Cuándo Leer |
|---------|-------------|-------------|
| **README.md** | Documentación general y deployment | **PRIMERO** |
| **QUICK-START.md** | Guía rápida para demo (15 min) | **Antes de configurar** |
| **DEMO-CHECKLIST.md** | Checklist completo pre/durante/post demo | **1 día antes del demo** |

### 📚 Documentación Detallada (`docs/`)

| Archivo | Descripción | Cuándo Leer |
|---------|-------------|-------------|
| **CONFIGURATION.md** | Guía detallada de configuración | Al configurar conexiones y blueprints |
| **TROUBLESHOOTING.md** | Solución de problemas comunes | Cuando algo falle |

### 🔧 Scripts de Automatización (`scripts/`)

| Script | Propósito | Ejecución |
|--------|-----------|-----------|
| **deploy.sh** | Deploy/stop/destroy del sistema | `./scripts/deploy.sh deploy` |
| **apply-db-fixes.sh** | Fixes automáticos de DB | Automático (via docker-compose) |
| **health-check.sh** | Verificación de salud | `./scripts/health-check.sh` |
| **sql/manual-fixes.sql** | SQL fixes (manual) | Si script automático falla |

### ⚙️ Configuración

| Archivo | Descripción |
|---------|-------------|
| **docker-compose.yml** | Configuración de servicios Docker |
| **.env.example** | Template de variables de entorno |
| **Makefile** | Shortcuts para comandos comunes |
| **.gitignore** | Archivos a ignorar en git |

### 📋 Ejemplos (`config/`)

| Archivo | Descripción |
|---------|-------------|
| **blueprints/demo-blueprint-example.json** | Ejemplo de blueprint para demo |

---

## 🎯 Flujo de Uso

```
┌─────────────────────────────────────────────────────────────┐
│                    INICIO                                     │
└───────────────────────┬─────────────────────────────────────┘
                        │
                        ▼
         ┌──────────────────────────┐
         │  1. Leer README.md       │
         │     y QUICK-START.md     │
         └──────────┬───────────────┘
                    │
                    ▼
         ┌──────────────────────────┐
         │  2. Configurar .env      │
         │     (tokens, endpoints)  │
         └──────────┬───────────────┘
                    │
                    ▼
         ┌──────────────────────────┐
         │  3. Deploy               │
         │     ./scripts/deploy.sh  │
         └──────────┬───────────────┘
                    │
                    ▼
         ┌──────────────────────────┐
         │  4. Health Check         │
         │     ./scripts/health-    │
         │     check.sh             │
         └──────────┬───────────────┘
                    │
                    ▼
         ┌──────────────────────────┐
         │  5. Configurar           │
         │     (GitLab, SonarQube,  │
         │      Blueprint)          │
         │     Ver CONFIGURATION.md │
         └──────────┬───────────────┘
                    │
                    ▼
         ┌──────────────────────────┐
         │  6. Sincronizar          │
         │     (20-30 min)          │
         └──────────┬───────────────┘
                    │
                    ▼
         ┌──────────────────────────┐
         │  7. Verificar Dashboards │
         │     en Grafana           │
         └──────────┬───────────────┘
                    │
                    ▼
         ┌──────────────────────────┐
         │  8. Demo!                │
         │     Ver DEMO-CHECKLIST.md│
         └──────────────────────────┘
```

---

## ⚡ Quick Commands

```bash
# Setup inicial
cp .env.example .env
vim .env

# Deploy completo
make deploy
# o
./scripts/deploy.sh deploy

# Verificar salud
make health
# o
./scripts/health-check.sh

# Ver estado
make status

# Logs en tiempo real
make logs-devlake -f

# Abrir interfaces
make open-config    # Config UI
make open-grafana   # Grafana

# Backup
make backup

# Ayuda
make help
```

---

## 📊 Arquitectura del Sistema

```
┌─────────────────────────────────────────────────────────────┐
│                     USUARIO / DEMO                            │
│                    (Browser: localhost)                       │
└───────┬──────────────────────┬──────────────────┬────────────┘
        │                      │                  │
        │ :5000                │ :5002            │ :5080
        ▼                      ▼                  ▼
┌───────────────┐    ┌─────────────────┐   ┌──────────────┐
│  Config UI    │    │    Grafana      │   │  DevLake API │
│               │    │  (Dashboards)   │   │              │
└───────┬───────┘    └────────┬────────┘   └──────┬───────┘
        │                     │                    │
        └─────────────────────┴────────────────────┘
                              │
                              ▼
                    ┌──────────────────┐
                    │  DevLake Core    │
                    │  (Sync Engine)   │
                    └─────────┬────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
┌──────────────┐    ┌──────────────┐     ┌────────────────┐
│   MySQL      │    │   GitLab     │     │   SonarQube    │
│ (Port: 5306) │    │ (VPN/SSL)    │     │   (VPN/SSL)    │
└──────────────┘    └──────────────┘     └────────────────┘
        │
        ▼
┌──────────────────┐
│   DB Fixes       │
│   (Automático)   │
└──────────────────┘
```

---

## 🎨 Características Principales

### ✅ Deployment Automatizado

- **Un comando**: `./scripts/deploy.sh deploy`
- **Health checks**: Automáticos en todos los servicios
- **DB fixes**: Se aplican automáticamente
- **Idempotente**: Puede ejecutarse múltiples veces

### ✅ Soporte para Banco Columbia

- **SSL/TLS**: Certificados self-signed soportados
- **VPN**: Funciona detrás de VPN corporativa
- **GitLab**: Self-hosted on-premise
- **SonarQube**: Self-hosted on-premise
- **Project keys largos**: Soportados (hasta 768 chars)
- **Components largos**: Soportados (hasta 65KB)

### ✅ Configuración Lista para Demo

- **Blueprint ejemplo**: Con repos seleccionados
- **Transformaciones DORA**: Pre-configuradas
- **Dashboards**: Optimizados para presentación
- **Date range**: 6 meses (suficiente para trends)

### ✅ Documentación Completa

- **README principal**: Setup y deployment
- **Quick start**: Demo en 15 minutos
- **Configuration**: Guía detallada paso a paso
- **Troubleshooting**: Solución de problemas
- **Checklist**: Para preparación de demo

### ✅ Herramientas de Debugging

- **Health check**: Verifica estado completo
- **Logs**: Acceso fácil y filtrado
- **Makefile**: Shortcuts para todo
- **SQL manual**: Para fixes específicos

---

## 📈 Métricas y Dashboards

### Dashboards Incluidos

1. **Executive Overview** ⭐⭐⭐
   - Métricas DORA principales
   - Trends de último mes
   - Comparación con benchmarks

2. **DORA Deep Dive** ⭐⭐⭐
   - Deployment Frequency
   - Lead Time for Changes
   - Change Failure Rate
   - MTTR

3. **Code Quality** ⭐⭐⭐
   - Technical Debt
   - Code Coverage
   - Bugs / Vulnerabilities
   - Security Hotspots

4. **Team Performance** ⭐⭐
   - Developer Velocity
   - PR Review Time
   - Top Contributors

### Datos Recolectados

**De GitLab:**
- Commits
- Merge Requests / Pull Requests
- Pipelines / CI/CD
- Issues
- Tags
- Branches

**De SonarQube:**
- Projects / Components
- Code Coverage
- Technical Debt
- Bugs / Vulnerabilities
- Security Hotspots
- Code Smells
- Duplications

---

## 🔒 Seguridad

### Incluido

- `.env.example` con documentación
- `.gitignore` para secrets
- Tokens no versionados
- SSL skip para self-signed certs

### Producción (TODO)

- [ ] Cambiar passwords default
- [ ] Usar certificados válidos
- [ ] Restringir puertos con firewall
- [ ] Implementar backups automáticos
- [ ] Monitoring de logs

---

## 🎯 Próximos Pasos

### Inmediato (Para Demo)

1. ✅ Configurar `.env` con tokens reales
2. ✅ Deploy: `./scripts/deploy.sh deploy`
3. ✅ Configurar GitLab y SonarQube en UI
4. ✅ Crear Blueprint con repos seleccionados
5. ✅ Ejecutar sincronización
6. ✅ Verificar dashboards
7. ✅ Practicar presentación

### Post-Demo (Implementación)

- [ ] Migrar a PostgreSQL (opcional)
- [ ] Configurar backups automáticos
- [ ] Implementar monitoring/alerting
- [ ] Agregar más data sources (Jira, etc)
- [ ] Customizar dashboards
- [ ] Configurar sync automático
- [ ] Deployment en cloud/k8s

---

## 📞 Soporte

### Recursos

- **Documentación Local**: Ver archivos en `docs/`
- **Apache DevLake**: https://devlake.apache.org/docs/
- **Community**: https://devlake.apache.org/community/
- **GitHub**: https://github.com/apache/incubator-devlake

### Contacto

- **Mikroways**: [Tu contacto aquí]
- **Issues**: Crear issue en repo interno

---

## 📝 Versión y Changelog

**Versión Actual**: 1.0  
**Apache DevLake**: v1.0.3-beta8  
**Última Actualización**: Noviembre 2025

**Cambios en v1.0:**
- ✅ Setup completo inicial
- ✅ Scripts de deployment automatizados
- ✅ DB fixes para Banco Columbia
- ✅ Documentación completa
- ✅ Ejemplo de blueprint
- ✅ Health checks
- ✅ Makefile con shortcuts

---

## 🙏 Créditos

**Desarrollado por**: Mikroways  
**Cliente**: Banco Columbia  
**Basado en**: Apache DevLake (Apache License 2.0)  
**Tecnologías**: Docker, MySQL, GitLab, SonarQube, Grafana

---

## 📜 Licencia

Este repositorio es específico para Banco Columbia.  
Apache DevLake está bajo Apache License 2.0.

---

1. `README.md` - Documentación general
2. `QUICK-START.md` - Guía rápida
3. `docs/TROUBLESHOOTING.md` - Solución de problemas
4. `./scripts/health-check.sh` - Verificación del sistema
