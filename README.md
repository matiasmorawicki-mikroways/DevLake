# Scripts - DevLake Demo

Este directorio contiene los scripts de automatización para deployment y mantenimiento.

## 📁 Estructura

```
scripts/
├── deploy.sh              # Script principal de deployment
├── apply-db-fixes.sh      # Fixes automáticos de base de datos
├── health-check.sh        # Verificación de salud del sistema
└── sql/
    └── manual-fixes.sql   # SQL para aplicar fixes manualmente
```

## 🚀 Scripts Principales

### deploy.sh

**Propósito:** Script principal para gestionar el ciclo de vida de DevLake.

**Comandos:**
```bash
./deploy.sh deploy      # Despliega todos los servicios
./deploy.sh stop        # Detiene servicios (mantiene datos)
./deploy.sh destroy     # Elimina TODO incluyendo volúmenes
./deploy.sh logs        # Muestra logs
./deploy.sh status      # Estado de servicios
./deploy.sh help        # Ayuda
```

**Qué hace `deploy`:**
1. Verifica requisitos (Docker, docker-compose, .env)
2. Verifica disponibilidad de puertos
3. Pull de imágenes Docker
4. Levanta servicios en orden (mysql → devlake → grafana → config-ui)
5. Espera a que servicios estén healthy
6. Ejecuta db-fixes automáticamente
7. Muestra URLs de acceso

**Uso:**
```bash
# Primera vez
cp .env.example .env
vim .env  # Configurar tokens
./deploy.sh deploy

# Ver estado
./deploy.sh status

# Detener
./deploy.sh stop
```

### apply-db-fixes.sh

**Propósito:** Aplica fixes de base de datos necesarios para soportar datos de SonarQube de Banco Columbia.

**Qué hace:**
1. Espera a que MySQL esté disponible
2. Espera a que migraciones de DevLake completen
3. Verifica estado actual de columnas
4. Aplica fixes solo si son necesarios:
   - Aumenta `project_key` a VARCHAR(768) en 6 tablas
   - Cambia `component` a TEXT en 4 tablas
   - Maneja PKs e índices especiales
5. Registra que fixes fueron aplicados
6. Muestra estadísticas finales

**Características:**
- **Idempotente**: Puede ejecutarse múltiples veces sin errores
- **Smart**: Solo modifica lo necesario
- **Safe**: Verifica estado antes de modificar

**Ejecución automática:**
Se ejecuta automáticamente cuando haces `./deploy.sh deploy` via el servicio `db-fixes` en docker-compose.

**Ejecución manual:**
```bash
# Via docker-compose
docker-compose up db-fixes

# Ver logs
docker-compose logs db-fixes
```

**Tablas modificadas:**

| Tabla | Columna | Cambio | Especial |
|-------|---------|--------|----------|
| _tool_sonarqube_issues | project_key | VARCHAR(768) | - |
| _tool_sonarqube_file_metrics | project_key | VARCHAR(768) | - |
| _tool_sonarqube_hotspots | project_key | VARCHAR(768) | - |
| _tool_sonarqube_projects | project_key | VARCHAR(768) | DROP/ADD PK |
| cq_issues | project_key | VARCHAR(768) | - |
| cq_file_metrics | project_key | VARCHAR(768) | - |
| _tool_sonarqube_hotspots | component | TEXT | - |
| _tool_sonarqube_issue_code_blocks | component | TEXT | - |
| _tool_sonarqube_issues | component | TEXT | - |
| cq_issue_code_blocks | component | TEXT | DROP/CREATE INDEX |

### health-check.sh

**Propósito:** Verifica que todos los componentes del sistema estén funcionando correctamente.

**Qué verifica:**
- Docker daemon
- Espacio en disco (>5GB recomendado)
- MySQL ping y tablas
- DB fixes aplicados
- Estado de containers (running/healthy)
- Endpoints HTTP:
  - DevLake API: http://localhost:5080/api/ping
  - Config UI: http://localhost:5000
  - Grafana: http://localhost:5002/api/health

**Salida:**
```
Verificando Docker... ✓ OK
Verificando espacio en disco... ✓ OK (45GB disponibles)
Verificando MySQL... ✓ OK
  → Verificando tablas... ✓ OK
  → Verificando DB fixes... ✓ OK
Verificando containers:
  → devlake-mysql... ✓ OK (healthy)
  → devlake-app... ✓ OK (healthy)
  → devlake-grafana... ✓ OK (healthy)
  → devlake-config-ui... ✓ OK (healthy)

Verificando DevLake API... ✓ OK (HTTP 200)
Verificando Config UI... ✓ OK (HTTP 200)
Verificando Grafana... ✓ OK (HTTP 200)

==========================================
Resumen del Health Check
==========================================
Exitosos:    12
Advertencias: 0
Errores:      0

✅ Sistema completamente saludable
```

**Exit codes:**
- `0` = Sistema OK (puede tener warnings)
- `1` = Sistema con errores críticos

**Uso:**
```bash
# Verificación completa
./health-check.sh

# En scripts
if ./health-check.sh; then
    echo "Sistema OK"
else
    echo "Sistema con problemas"
fi
```

**Cuándo ejecutar:**
- Después de cada deploy
- Antes de una demo
- Al troubleshootear problemas
- Periódicamente para monitoreo

## 📄 SQL Scripts

### sql/manual-fixes.sql

**Propósito:** Versión SQL pura de los fixes, para aplicar manualmente si el script automatizado falla.

**Cuándo usar:**
- Script automatizado falló
- Necesitas aplicar solo algunos fixes
- Debugging de problemas de DB
- Rollback de cambios (incluye queries)

**Aplicar manualmente:**
```bash
# Desde host
docker-compose exec -T mysql mysql -umerico -pmerico lake < scripts/sql/manual-fixes.sql

# Desde container
docker-compose exec mysql bash
mysql -umerico -pmerico lake < /scripts/sql/manual-fixes.sql
```

**Contenido:**
- Parte 1: Fixes de `project_key`
- Parte 2: Fixes de `component`
- Parte 3: Registro de tracking
- Verificación queries
- Rollback queries (comentadas)

**Verificar aplicación:**
```bash
docker-compose exec mysql mysql -umerico -pmerico lake -e "
  SELECT * FROM _devlake_custom_fixes;
"
```

## 🔧 Uso con Make

Los scripts también pueden ejecutarse via Makefile:

```bash
# Deployment
make deploy

# Health check
make health

# Status
make status

# Logs
make logs

# Re-aplicar DB fixes
make fix-db
```

Ver `Makefile` para lista completa de comandos.

## 🐛 Debugging

### Ver logs de scripts

**Deploy script:**
```bash
# El output va a stdout/stderr directamente
./deploy.sh deploy 2>&1 | tee deploy.log
```

**DB fixes script:**
```bash
# Via docker-compose
docker-compose logs db-fixes

# En tiempo real
docker-compose up db-fixes
```

**Health check:**
```bash
# Verbose output
bash -x ./health-check.sh
```

### Modificar scripts

Todos los scripts están en bash y son fácilmente modificables:

```bash
# Editar
vim scripts/deploy.sh

# Hacer ejecutable si es necesario
chmod +x scripts/deploy.sh

# Testear
./scripts/deploy.sh help
```

### Variables de entorno

Scripts respetan variables de `.env`:

```bash
# Cambiar defaults
export MYSQL_HOST=custom-host
export MYSQL_PORT=3306

# Ejecutar
./scripts/apply-db-fixes.sh
```

## 📋 Checklist de Desarrollo

Si modificas los scripts:

- [ ] Mantener idempotencia
- [ ] Agregar logging claro
- [ ] Manejar errores apropiadamente
- [ ] Documentar cambios en este README
- [ ] Testear en ambiente limpio
- [ ] Considerar backward compatibility

## 🆘 Troubleshooting

### Script falla con "permission denied"

```bash
chmod +x scripts/*.sh
```

### Script no encuentra docker-compose

```bash
# Verificar instalación
which docker-compose
docker compose version  # Syntax alternativa

# Modificar script para usar 'docker compose'
```

### DB fixes no se aplican

```bash
# Ver logs detallados
docker-compose up db-fixes

# Aplicar manualmente
docker-compose exec -T mysql mysql -umerico -pmerico lake < scripts/sql/manual-fixes.sql

# Verificar
docker-compose exec mysql mysql -umerico -pmerico lake -e "
  SELECT COLUMN_TYPE FROM INFORMATION_SCHEMA.COLUMNS 
  WHERE TABLE_NAME='_tool_sonarqube_projects' 
  AND COLUMN_NAME='project_key';
"
```

## 📚 Referencias

- [Bash Best Practices](https://bertvv.github.io/cheat-sheets/Bash.html)
- [Docker Compose CLI](https://docs.docker.com/compose/reference/)
- [MySQL CLI](https://dev.mysql.com/doc/refman/8.0/en/mysql.html)

---
