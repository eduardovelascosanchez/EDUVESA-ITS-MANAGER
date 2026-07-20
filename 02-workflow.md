# 02 · Workflow técnico paso a paso

**Herramientas integradas:** Claude Desktop + Claude Project + Artifacts (3 de la suite; el mínimo exigido es 2).
**Frecuencia de uso:** semanal (auditoría) + bajo demanda (reportes especiales).
**Usos documentados en semana 6:** 2 (ver `03-capturas/`).

---

## Diagrama general

```
Google Drive (rosters, vigencias, cursos)
        │
        ▼
[1] Claude Desktop ──lee y estructura──▶ datos normalizados
        │
        ▼
[2] Project "AHA Training Central" ──aplica reglas──▶ clasificación semáforo
        │
        ▼
[3] Artifacts ──genera──▶ Panel de 7 módulos + reporte de acciones
        │
        ▼
[4] VERIFICACIÓN HUMANA ──coteja──▶ AHA Instructor Network (fuente oficial)
        │
        ▼
[5] Decisión y comunicación (siempre firmadas por mí)
```

---

## Paso 1 — Ingesta de datos (Claude Desktop)

| Elemento | Detalle |
|---|---|
| **Herramienta** | Claude Desktop con conector de Google Drive |
| **Prompt (general)** | "Lee los archivos de vigencias e instructores de la carpeta de la red. Extrae por instructor: disciplina(s), fecha de emisión, fecha de vencimiento y Training Site. Marca explícitamente cualquier dato que no encuentres en los archivos — no lo infieras." |
| **Entrada** | Rosters y registros administrativos de la red en Drive. **Sin PHI:** son datos de instructores adultos (nombre profesional, disciplina, fechas de credencial), no de pacientes. |
| **Salida** | Tabla normalizada de instructores con sus vigencias por disciplina. |
| **Verificación** | Conteo cruzado: el total de instructores extraídos debe coincidir con el roster maestro. Todo campo marcado como "no encontrado" se resuelve manualmente. |

## Paso 2 — Clasificación con reglas de negocio (Claude Project)

| Elemento | Detalle |
|---|---|
| **Herramienta** | Project "AHA Training Central" (contexto persistente) |
| **Prompt (general)** | "Con las reglas de vigencia de la red que están en el contexto del Project, clasifica cada instructor en verde (vigente), amarillo (vence en menos de 90 días) o rojo (vencido). Genera la lista priorizada de acciones: a quién contactar, para qué disciplina y con qué urgencia." |
| **Entrada** | Tabla del Paso 1 + conocimiento del Project (periodos de vigencia por disciplina, requisitos de renovación, estructura y contactos de la red). |
| **Salida** | Clasificación semáforo + lista de acciones priorizadas. |
| **Verificación** | Muestreo: reviso manualmente el cálculo de al menos 3 casos (uno por color). Las reglas del Project se auditan contra la normativa AHA vigente cada vez que la AHA publica cambios. |

## Paso 3 — Panel y reportes (Artifacts)

| Elemento | Detalle |
|---|---|
| **Herramienta** | Artifacts |
| **Prompt (general)** | "Actualiza el panel de vigencias con estos datos y genera el reporte ejecutivo del ciclo: resumen por Training Site, casos rojos con acción inmediata y proyección de vencimientos a 90 días." |
| **Entrada** | Salida clasificada del Paso 2. |
| **Salida** | Aplicación web de 7 módulos (Panel/Semáforo, Sites, Cursos, Instructores, Cuotas, Recordatorios, Reportes) con persistencia local + reporte ejecutivo del ciclo. |
| **Verificación** | Los totales del panel deben cuadrar con la tabla origen (suma verde+amarillo+rojo = total de instructores). |

## Paso 4 — Verificación contra fuente oficial (humano)

| Elemento | Detalle |
|---|---|
| **Herramienta** | Ninguna de IA: AHA Instructor Network (fuente oficial) + criterio propio |
| **Proceso** | Todo caso 🔴 y todo caso que dispare una comunicación formal se coteja contra el registro oficial de la AHA antes de actuar. |
| **Regla** | **Ningún dato crítico se da por bueno solo porque lo dijo el modelo.** Este paso es innegociable y está diseñado explícitamente contra alucinaciones. |

## Paso 5 — Decisión y comunicación (humano)

Las comunicaciones a Training Sites e instructores las redacto (con o sin ayuda de Claude), las reviso y las firmo yo. Los casos complejos —un site en conflicto, un instructor en situación irregular— se resuelven en conversación directa con las coordinadoras de la red, no con el modelo.

---

## Manejo de riesgos y alucinaciones (resumen)

1. **Instrucción anti-inferencia** en el prompt de ingesta: lo no encontrado se marca, no se inventa.
2. **Conteos de control** en cada transición de paso (nada se pierde ni se duplica).
3. **Muestreo manual** de la clasificación en cada ciclo.
4. **Verificación obligatoria contra fuente oficial** para todo caso crítico.
5. **Decisión siempre humana**: Claude propone, yo decido y firmo.
