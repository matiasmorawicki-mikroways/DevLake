# Guía Rápida: Configuración Demo Banco Columbia

## 🚀 Quick Start (15 minutos)

### 1. Setup Inicial (3 min)

```bash
# Clonar/descargar el repo
cd devlake-demo-bancolombia

# Configurar credenciales
cp .env.example .env
vim .env  # Editar con tus tokens

# Desplegar
./scripts/deploy.sh deploy
```

### 2. Verificar (2 min)

```bash
# Health check
./scripts/health-check.sh

# O manual
make status
make health
```

### 3. Configurar Conexiones (5 min)

Accede a http://localhost:5000

**GitLab:**
- Name: `Banco Columbia GitLab`
- Endpoint: `https://gitlab.bancocolumbia.cloud`
- Token: `glpat-...` (de tu .env)
- Test Connection → Save

**SonarQube:**
- Name: `Banco Columbia SonarQube`
- Endpoint: `https://sonarqube.bancocolumbia.cloud`
- Token: `squ_...` (de tu .env)
- Test Connection → Save

### 4. Crear Blueprint (5 min)

**Configuración recomendada:**

```yaml
Name: Banco Columbia - Demo Q4 2024

Repos (seleccionar 5-10):
  Backend:
    - payment-service
    - user-service
    - notification-service
  Frontend:
    - banking-portal
  DevOps:
    - k8s-manifests

Date Range:
  From: 2024-06-01
  To: Today

Branches:
  - main
  - master
  - develop
  - staging

Sync: Manual (para demo)
```

**Transformaciones DORA:**

```json
{
  "deploymentPattern": "^(v\\d+\\.\\d+\\.\\d+|release-.*)",
  "productionBranches": ["main", "master", "production"],
  "incidentLabels": ["incident", "outage", "critical"],
  "bugLabels": ["bug", "defect", "hotfix"]
}
```

### 5. Sincronizar (15-30 min)

- Click **Run Now** en el Blueprint
- Monitorea: `make logs-devlake -f`
- Tiempo: ~20min para 5 repos con 6 meses

## 📊 Selección de Repositorios

### Criterios Obligatorios

✅ **INCLUIR repos que tengan:**
- Commits en últimos 30 días
- CI/CD activo
- 10+ PRs cerrados en últimos 3 meses
- SonarQube configurado
- Multiple developers (3+)

❌ **EVITAR repos que sean:**
- Archivados
- Solo documentación
- Forks sin actividad
- <50 commits totales

### Repos Recomendados por Categoría

**Backend/APIs (3-4 repos):**
```
Ejemplo:
- backend/payment-service
- backend/user-service
- backend/auth-service
- backend/notification-service
```

**Frontend (1-2 repos):**
```
Ejemplo:
- frontend/banking-portal
- frontend/admin-dashboard
```

**DevOps/Infrastructure (1 repo):**
```
Ejemplo:
- devops/k8s-manifests
- devops/terraform-modules
```

**Total recomendado: 5-7 repos para demo efectivo**

## 🎯 Configuración DORA

### Deployment Detection

**Opción 1: Tags (Recomendado)**
```
Pattern: ^(v\d+\.\d+\.\d+|release-.*)
Branches: main, master, production

Detecta:
- v1.2.3
- v2.0.0-rc1
- release-2024.11.25
```

**Opción 2: CI/CD Pipelines**
```
Stage: deploy, production, release
Status: success
```

**Opción 3: Merge Events**
```
Trigger: merge
Target: main, master, production
```

**Para Banco Columbia:** Usa Tags + CI/CD combinados.

### Issue Classification

**Incidents/Outages:**
```json
{
  "labels": ["incident", "outage", "production-issue", "critical"],
  "titlePattern": "\\[INCIDENT\\]|\\[PROD\\]|URGENT:"
}
```

**Bugs:**
```json
{
  "labels": ["bug", "defect", "hotfix"],
  "titlePattern": "^(bug|fix|hotfix):"
}
```

### Métricas DORA Esperadas

**Para demo efectivo, busca proyectos con:**
- Deployment Frequency: 1/week o mejor
- Lead Time: <7 días
- Change Failure Rate: <30%
- MTTR: <24 horas

**Benchmarks de industria:**
```
Elite:    DF=daily,      LT<1h,      CFR<15%,  MTTR<1h
High:     DF=weekly,     LT<1day,    CFR<30%,  MTTR<1day
Medium:   DF=monthly,    LT<1week,   CFR<45%,  MTTR<1week
Low:      DF<6months,    LT>1week,   CFR>45%,  MTTR>1week
```

## 📈 Dashboards para Demo

### Orden Recomendado de Presentación

**1. Executive Overview (3 min) ⭐⭐⭐**
- Scorecard con métricas clave
- Trends de último mes
- Comparación con benchmarks

**2. DORA Deep Dive (5 min) ⭐⭐⭐**
- Deployment Frequency por repo
- Lead Time distribution
- Change Failure Rate timeline
- MTTR per incident

**3. Code Quality (5 min) ⭐⭐⭐**
- Technical Debt trend
- Coverage por proyecto
- Bugs/Vulnerabilities severity
- Code Smells evolution

**4. Team Performance (3 min) ⭐⭐**
- Developer velocity
- PR review time
- Top contributors

**5. Q&A (4 min)**

### Dashboards en Grafana

Accede a: http://localhost:5002

**Login:**
- User: `admin`
- Pass: `admin` (cambiar en primer acceso)

**Ubicación:** Dashboards > Browse > DevLake

## 🎨 Tips para Demo Efectiva

### Pre-Demo Checklist

**1 día antes:**
- [ ] Sync completo ejecutado
- [ ] Todos los dashboards funcionando
- [ ] Screenshots de backup tomadas
- [ ] Talking points preparados

**2 horas antes:**
- [ ] Sync incremental para datos frescos
- [ ] `./scripts/health-check.sh` OK
- [ ] Tabs de dashboards abiertos
- [ ] Browser cache limpio

### Durante la Demo

**DO's:**
- ✅ Empezar con contexto de negocio
- ✅ Mostrar datos reales del cliente
- ✅ Comparar con benchmarks de industria
- ✅ Identificar insights accionables
- ✅ Responder preguntas con datos

**DON'Ts:**
- ❌ Entrar en detalles técnicos innecesarios
- ❌ Disculparse por métricas "malas"
- ❌ Prometer features no implementados
- ❌ Hablar mal de herramientas actuales del cliente

### Mensajes Clave

**Value Props:**
1. "Visibilidad end-to-end del proceso de desarrollo"
2. "Data-driven decision making con métricas de industria"
3. "Identificación proactiva de bottlenecks"
4. "Mejora continua basada en evidencia"

**Diferenciadores:**
1. Open source (no vendor lock-in)
2. Multi-fuente (GitLab + SonarQube + más)
3. DORA metrics out-of-the-box
4. Customizable y extensible

## 🔄 Mantenimiento

### Sincronización Regular

**Para demo persistente:**
```bash
# Editar .env
SYNC_CRON=0 2 * * *  # Diario 2 AM

# O manual
curl -X POST http://localhost:5080/api/blueprints/1/trigger
```

### Limpieza

```bash
# Limpiar logs
make clean-logs

# Backup antes de limpiar datos
make backup

# Ver tamaño de DB
make stats
```

## 🆘 Problemas Comunes

### "MySQL connection refused"
```bash
./scripts/deploy.sh restart
```

### "SSL certificate error"
```bash
# Verificar en .env:
IN_SECURE_SKIP_VERIFY=true
```

### "401 Unauthorized"
```bash
# Verificar tokens en .env
# Regenerar si es necesario
```

### "Sync muy lento"
```bash
# Reducir scope:
# - Menos repos (5-7)
# - 6 meses en vez de todo el histórico
# - Solo branches principales
```

### Ver guía completa:
```bash
cat docs/TROUBLESHOOTING.md
```

## 📞 Comandos Útiles

```bash
# Status
make status

# Health check
./scripts/health-check.sh

# Logs en tiempo real
make logs-devlake -f

# Abrir UI
make open-config    # Config UI
make open-grafana   # Grafana

# Backup
make backup

# Reiniciar todo
make restart

# Ver ayuda
make help
```

## 📚 Documentación Completa

- `README.md` - Documentación general y deployment
- `docs/CONFIGURATION.md` - Guía detallada de configuración
- `docs/TROUBLESHOOTING.md` - Resolución de problemas
- `.env.example` - Todas las variables disponibles

## 🎯 Objetivo Final

**Al terminar el demo, el cliente debe:**
1. Reconocer sus propios datos y proyectos
2. Entender las métricas DORA y su valor
3. Identificar al menos 2-3 insights accionables
4. Querer implementar DevLake en su organización
5. Agendar follow-up para discutir implementación

**Success metrics:**
- Engagement durante presentación
- Preguntas específicas sobre sus datos
- Solicitud de access/trial
- Follow-up meeting agendado

---

