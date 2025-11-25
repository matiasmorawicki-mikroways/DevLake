# Checklist Demo - Banco Columbia

## 📋 Pre-Demo (1-2 días antes)

### Infraestructura
- [ ] Repositorio clonado/descargado
- [ ] `.env` configurado con tokens válidos
- [ ] Deployment ejecutado: `./scripts/deploy.sh deploy`
- [ ] Health check OK: `./scripts/health-check.sh`
- [ ] Acceso a VPN de Banco Columbia confirmado

### Conexiones
- [ ] GitLab connection configurada y testeada
- [ ] SonarQube connection configurada y testeada
- [ ] Tokens con permisos correctos verificados

### Datos
- [ ] 5-7 repositorios seleccionados (ver criterios en QUICK-START.md)
- [ ] Blueprint creado con configuración correcta
- [ ] Transformaciones DORA configuradas
- [ ] Primera sincronización completa ejecutada (20-30 min)
- [ ] Datos visibles en Grafana

### Dashboards
- [ ] Executive Overview accesible
- [ ] DORA Metrics dashboard con datos
- [ ] Code Quality dashboard con datos de SonarQube
- [ ] Team Performance dashboard poblado
- [ ] Variables de Grafana funcionando

### Backup & Recovery
- [ ] Backup de DB creado: `make backup`
- [ ] Screenshots de dashboards tomadas
- [ ] Datos de ejemplo documentados

## 🎯 Día Anterior a Demo

### Verificación Técnica
- [ ] Sincronización incremental ejecutada
- [ ] Todos los servicios UP: `make status`
- [ ] Puertos accesibles: 5000, 5002, 5080
- [ ] No hay errores en logs: `make logs | grep -i error`
- [ ] DB fixes verificados: `docker-compose logs db-fixes`

### Preparación de Contenido
- [ ] Talking points escritos (ver QUICK-START.md)
- [ ] Insights clave identificados en los datos
- [ ] Comparaciones con benchmarks preparadas
- [ ] Preguntas frecuentes anticipadas

### Ambiente
- [ ] Laptop/PC con suficiente carga
- [ ] Conexión a internet estable
- [ ] VPN configurada y funcionando
- [ ] Proyector/pantalla testeado
- [ ] Audio funcionando (si aplica)

## ⏰ 2 Horas Antes de Demo

### Refresh de Datos
- [ ] Conectado a VPN de Banco Columbia
- [ ] Health check: `./scripts/health-check.sh`
- [ ] Sync incremental ejecutado (5-10 min)
- [ ] Nuevos datos confirmados en dashboards

### Browser Setup
- [ ] Cache limpiado
- [ ] Tabs pre-abiertos:
  - [ ] Config UI: http://localhost:5000
  - [ ] Grafana: http://localhost:5002
  - [ ] Executive Overview dashboard
  - [ ] DORA Metrics dashboard
  - [ ] Code Quality dashboard
- [ ] Login en Grafana hecho
- [ ] Zoom/resolución ajustados para proyector

### Contingencia
- [ ] Screenshots de respaldo en carpeta accesible
- [ ] Plan B si falla conexión (mostrar desde screenshots)
- [ ] Contacto de soporte técnico disponible

## 🎤 Durante Demo

### Inicio (2 min)
- [ ] Bienvenida y presentación
- [ ] Contexto: "Métricas de DevOps con sus datos reales"
- [ ] Agenda rápida

### Executive Overview (3 min)
- [ ] Mostrar dashboard principal
- [ ] Destacar Deployment Frequency
- [ ] Comentar Lead Time
- [ ] Mencionar CFR y MTTR

### DORA Deep Dive (5 min)
- [ ] Explicar cada métrica DORA
- [ ] Mostrar trends
- [ ] Comparar con benchmarks de industria
- [ ] Identificar repos top performers

### Code Quality (5 min)
- [ ] Technical Debt overview
- [ ] Coverage trends
- [ ] Bugs/Vulnerabilities por proyecto
- [ ] Correlación code quality ↔ deployments

### Team Performance (3 min)
- [ ] Velocity por developer
- [ ] PR review time
- [ ] Bottlenecks identificados

### Value Props (2 min)
- [ ] Visibilidad end-to-end
- [ ] Data-driven decisions
- [ ] Mejora continua
- [ ] Alineación con estándares

### Q&A (Tiempo restante)
- [ ] Responder preguntas con datos
- [ ] Ofrecer deep dives adicionales
- [ ] Discutir próximos pasos

## ✅ Post-Demo

### Inmediato (Durante/después de reunión)
- [ ] Notas de preguntas tomadas
- [ ] Feedback capturado
- [ ] Follow-up agendado (si aplicable)
- [ ] Insights adicionales prometidos anotados

### Mismo Día
- [ ] Email de follow-up enviado
- [ ] Screenshots/datos compartidos (si solicitado)
- [ ] Próximos pasos confirmados
- [ ] Feedback interno documentado

### 24-48 Horas
- [ ] Análisis adicional generado (si prometido)
- [ ] Propuesta de implementación preparada
- [ ] Timeline de próximos pasos definido

## 🎯 Métricas de Éxito

### Durante Demo
- [ ] Audience engaged (preguntas, interés visual)
- [ ] Cliente reconoce sus datos
- [ ] Al menos 2-3 insights identificados
- [ ] Cero downtime/problemas técnicos

### Post-Demo
- [ ] Cliente solicita acceso/trial
- [ ] Follow-up meeting agendado
- [ ] Preguntas sobre implementación
- [ ] Presupuesto/timeline discutido
- [ ] Referencia a stakeholders adicionales

## 🆘 Plan de Contingencia

### Si servicios no responden
- [ ] Mostrar desde screenshots pre-tomados
- [ ] Explicar que es network/VPN
- [ ] Continuar con data estático

### Si datos no cargan
- [ ] Tener ejemplos de otro cliente (anonimizado)
- [ ] Focus en capabilities vs datos específicos
- [ ] Ofrecer demo detallado post-meeting

### Si preguntas difíciles
- [ ] "Excelente pregunta, déjame anotarla"
- [ ] "Profundicemos en eso después del demo"
- [ ] "Necesito validar eso con el equipo"

### Si comparaciones con competencia
- [ ] Focus en strengths de DevLake
- [ ] Open source advantage
- [ ] Customización y extensibilidad
- [ ] Community support

## 📞 Contactos de Emergencia

**Durante Demo:**
- Soporte Mikroways: [contacto]
- Backup presenter: [nombre]

**Post-Demo:**
- Product owner: [contacto]
- Technical lead: [contacto]

## 📝 Notas

### Insights Identificados
```
[Espacio para anotar insights durante revisión de datos]

1. 
2. 
3. 
```

### Preguntas Recibidas
```
[Espacio para anotar preguntas durante demo]

1. 
2. 
3. 
```

### Action Items
```
[Espacio para follow-up items]

1. 
2. 
3. 
```

---

