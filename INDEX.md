# 📑 Índice de Navegación - DevLake Demo Banco Columbia

Este archivo te guía hacia la documentación correcta según tu necesidad.

## 🎯 "Solo quiero deployar rápido"

1. **[QUICK-START.md](QUICK-START.md)** - 15 minutos para tener todo funcionando
2. **[DEMO-CHECKLIST.md](DEMO-CHECKLIST.md)** - Checklist pre/durante/post demo

## 📖 "Quiero entender todo el proyecto"

1. **[PROJECT-OVERVIEW.md](PROJECT-OVERVIEW.md)** - Vista general completa
2. **[README.md](README.md)** - Documentación principal y deployment
3. **[docs/CONFIGURATION.md](docs/CONFIGURATION.md)** - Configuración detallada

## 🔧 "Tengo problemas técnicos"

1. **[docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)** - Solución de problemas
2. **[scripts/README.md](scripts/README.md)** - Documentación de scripts
3. Ejecutar: `./scripts/health-check.sh`

## 🚀 "Voy a hacer el deployment"

### Paso 1: Preparación
- [ ] Leer [README.md](README.md) sección "Prerrequisitos"
- [ ] Copiar `.env.example` a `.env`
- [ ] Configurar tokens en `.env`

### Paso 2: Deployment
- [ ] Ejecutar: `./scripts/deploy.sh deploy`
- [ ] Verificar: `./scripts/health-check.sh`

### Paso 3: Configuración
- [ ] Seguir [docs/CONFIGURATION.md](docs/CONFIGURATION.md)
- [ ] Crear conexiones (GitLab, SonarQube)
- [ ] Crear Blueprint
- [ ] Ejecutar sincronización

### Paso 4: Verificación
- [ ] Abrir Grafana: http://localhost:5002
- [ ] Verificar dashboards tienen datos
- [ ] Tomar screenshots de backup

## 🎤 "Voy a presentar el demo"

### Pre-Demo
1. **[DEMO-CHECKLIST.md](DEMO-CHECKLIST.md)** - Checklist completo
2. **[QUICK-START.md](QUICK-START.md)** sección "Tips para Demo"

### Durante Demo
- Orden recomendado en [QUICK-START.md](QUICK-START.md) sección "Dashboards"
- Talking points en [docs/CONFIGURATION.md](docs/CONFIGURATION.md)

### Post-Demo
- Follow-up checklist en [DEMO-CHECKLIST.md](DEMO-CHECKLIST.md)

## 🛠️ "Quiero customizar o desarrollar"

- **[scripts/README.md](scripts/README.md)** - Documentación de scripts
- **[docker-compose.yml](docker-compose.yml)** - Configuración de servicios
- **[config/blueprints/](config/blueprints/)** - Ejemplos de blueprints
- **[scripts/sql/manual-fixes.sql](scripts/sql/manual-fixes.sql)** - SQL queries

## 📚 Guía por Rol

### Soy DevOps / SysAdmin
Leer en orden:
1. [README.md](README.md) - Setup y arquitectura
2. [scripts/README.md](scripts/README.md) - Scripts y automatización
3. [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md) - Debugging

### Soy Developer / Technical Lead
Leer en orden:
1. [PROJECT-OVERVIEW.md](PROJECT-OVERVIEW.md) - Visión general
2. [docs/CONFIGURATION.md](docs/CONFIGURATION.md) - Métricas y transformaciones
3. [QUICK-START.md](QUICK-START.md) - Configuración rápida

### Soy Sales / Account Manager
Leer en orden:
1. [PROJECT-OVERVIEW.md](PROJECT-OVERVIEW.md) - Value props y features
2. [DEMO-CHECKLIST.md](DEMO-CHECKLIST.md) - Preparación de demo
3. [QUICK-START.md](QUICK-START.md) - Tips de presentación

### Soy Manager / Decision Maker
Leer en orden:
1. [PROJECT-OVERVIEW.md](PROJECT-OVERVIEW.md) sección "Características"
2. [docs/CONFIGURATION.md](docs/CONFIGURATION.md) sección "Métricas DORA"
3. [README.md](README.md) sección "Servicios"

## 🗺️ Mapa del Repositorio

```
devlake-demo-bancolombia/
│
├── 📄 Documentación Principal
│   ├── README.md                    ← Empezar aquí
│   ├── PROJECT-OVERVIEW.md          ← Vista general completa
│   ├── QUICK-START.md               ← Guía rápida (15 min)
│   ├── DEMO-CHECKLIST.md            ← Checklist pre/durante/post
│   └── INDEX.md                     ← Este archivo
│
├── 📁 docs/
│   ├── CONFIGURATION.md             ← Configuración detallada
│   └── TROUBLESHOOTING.md           ← Solución de problemas
│
├── 🔧 scripts/
│   ├── README.md                    ← Documentación de scripts
│   ├── deploy.sh                    ← Script principal ⭐
│   ├── apply-db-fixes.sh            ← DB fixes automáticos
│   ├── health-check.sh              ← Verificación de salud
│   └── sql/
│       └── manual-fixes.sql         ← SQL manual (fallback)
│
├── ⚙️ Configuración
│   ├── docker-compose.yml           ← Servicios Docker
│   ├── .env.example                 ← Template de variables
│   ├── Makefile                     ← Shortcuts útiles
│   └── .gitignore                   ← Exclusiones de git
│
└── 📋 config/
    └── blueprints/
        └── demo-blueprint-example.json  ← Ejemplo de blueprint
```

## ⚡ Comandos Más Usados

```bash
# Deployment
./scripts/deploy.sh deploy
make deploy

# Verificación
./scripts/health-check.sh
make health

# Estado
./scripts/deploy.sh status
make status

# Logs
make logs-devlake -f

# Interfaces
make open-config    # http://localhost:5000
make open-grafana   # http://localhost:5002

# Backup
make backup

# Ayuda completa
make help
```

## 🆘 Flujos de Problemas

### "El deployment falló"
1. Ver logs: `make logs | grep -i error`
2. Consultar [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)
3. Ejecutar: `./scripts/health-check.sh`

### "Los datos no se sincronizan"
1. Verificar conexiones en Config UI
2. Ver logs: `make logs-devlake -f`
3. Consultar [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md) sección "Sync"

### "Los dashboards están vacíos"
1. Verificar que sync completó: Config UI > Blueprints
2. Verificar datos en DB: `make stats`
3. Esperar a que Grafana actualice (puede tomar 1-2 min)

### "Problemas durante el demo"
1. Usar screenshots de backup
2. Consultar [DEMO-CHECKLIST.md](DEMO-CHECKLIST.md) sección "Plan de Contingencia"
3. Focus en capabilities vs datos específicos

## 🎓 Aprendizaje Progresivo

### Nivel 1: Básico (30 min)
- [ ] [README.md](README.md) - Intro y deployment
- [ ] [QUICK-START.md](QUICK-START.md) - Setup rápido
- [ ] Deployar el sistema

### Nivel 2: Intermedio (2 horas)
- [ ] [docs/CONFIGURATION.md](docs/CONFIGURATION.md) - Configuración
- [ ] Configurar conexiones y blueprint
- [ ] Ejecutar primera sincronización
- [ ] Explorar dashboards

### Nivel 3: Avanzado (4+ horas)
- [ ] [PROJECT-OVERVIEW.md](PROJECT-OVERVIEW.md) - Arquitectura completa
- [ ] [scripts/README.md](scripts/README.md) - Entender automatización
- [ ] [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md) - Debugging
- [ ] Customizar configuración

### Nivel 4: Experto (Semanas)
- [ ] Modificar scripts
- [ ] Crear dashboards personalizados
- [ ] Optimizar performance
- [ ] Implementar en producción

## 📞 Necesitas Ayuda

### Primero Intenta
1. Buscar en [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)
2. Ejecutar `./scripts/health-check.sh`
3. Revisar logs: `make logs | grep -i error`

### Si Aún Tienes Problemas
- **Interno Mikroways**: [Contacto interno]
- **Apache DevLake Community**: https://devlake.apache.org/community/
- **GitHub Issues**: https://github.com/apache/incubator-devlake

### Información a Proveer
- Versión: DevLake v1.0.3-beta8
- OS y Docker version
- Logs relevantes
- Pasos para reproducir

---

## ✅ Quick Checklist por Situación

### "Primera vez que uso esto"
- [ ] Leer [README.md](README.md)
- [ ] Leer [QUICK-START.md](QUICK-START.md)
- [ ] Configurar `.env`
- [ ] Ejecutar `./scripts/deploy.sh deploy`
- [ ] Seguir [docs/CONFIGURATION.md](docs/CONFIGURATION.md)

### "Tengo que hacer una demo mañana"
- [ ] Leer [DEMO-CHECKLIST.md](DEMO-CHECKLIST.md)
- [ ] Verificar deployment: `./scripts/health-check.sh`
- [ ] Sync incremental
- [ ] Tomar screenshots
- [ ] Practicar presentación

### "Algo se rompió"
- [ ] `./scripts/health-check.sh`
- [ ] Consultar [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)
- [ ] Ver logs: `make logs`
- [ ] Intentar `make restart`

### "Quiero customizar"
- [ ] Leer [scripts/README.md](scripts/README.md)
- [ ] Leer [docs/CONFIGURATION.md](docs/CONFIGURATION.md)
- [ ] Revisar ejemplos en `config/`
- [ ] Modificar y testear

---
