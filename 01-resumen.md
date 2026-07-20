# 01 · Resumen del proyecto

**Proyecto:** Semáforo de Vigencias — workflow compuesto para la gestión de una red de Training Sites AHA
**Autor:** Dr. Eduardo Javier Velasco Sánchez · Pediatra intensivista · Faculty Internacional AHA (BLS/ACLS/PALS/NRP)
**Curso:** Haz Magia con Claude · SimAcademy · Semana 6 — Proyecto final (individual)

## Qué resuelve

Coordino una red de aproximadamente 30 Training Sites AHA en México y Latinoamérica (CAMICC, CAMED, ACSUR, Código Azul, FACE Institute, entre otros). El seguimiento de vigencias de instructores en cuatro disciplinas (BLS, ACLS, PALS, NRP), sus fechas de renovación, cuotas y cumplimiento normativo se realizaba de forma manual, con información dispersa en múltiples archivos de Google Drive.

El riesgo operativo es concreto: un instructor impartiendo cursos con credencial vencida invalida certificaciones y expone a la red ante la AHA. El riesgo regulatorio también: la implementación obligatoria de NRP 9ª edición tenía fecha límite del 1 de junio de 2026, y no existía visibilidad centralizada de qué instructores habían migrado.

## Cómo lo resuelve

Un workflow compuesto que integra **tres herramientas** de la suite Anthropic:

1. **Claude Desktop** lee y cruza directamente desde Google Drive los rosters, registros de cursos y fechas de vigencia de la red.
2. **Claude Project "AHA Training Central"** aporta el contexto persistente: estructura de la red, reglas de vigencia por disciplina, contactos de coordinación y decisiones previas.
3. **Artifacts** genera y mantiene la aplicación web de 7 módulos (Panel/Semáforo, Sites, Cursos, Instructores, Cuotas, Recordatorios, Reportes) y los reportes ejecutivos de acción.

El resultado de cada ciclo es un semáforo por instructor (🟢 vigente · 🟡 vence en <90 días · 🔴 vencido) y una lista priorizada de acciones. El paso final del workflow no es de Claude: es la verificación humana de todo caso crítico contra la fuente oficial (AHA Instructor Network) antes de cualquier comunicación o decisión.

## Impacto

- Auditoría de vigencias: de **una jornada trimestral (~6 h) a ~15 minutos semanales**.
- Detección **proactiva** de la brecha de cumplimiento NRP 9ª edición antes del deadline regulatorio, con lista nominal de instructores pendientes de migración.
- Hallazgo colateral del análisis cruzado: un segmento corporativo HeartSaver no explotado.
- **Cero PHI por diseño:** el workflow solo procesa datos administrativos de instructores adultos, en el marco de la coordinación de la red. Ningún dato de paciente entra a la herramienta.

**Transferencia:** este workflow ya es parte de mi rutina semanal y seguirá en uso mientras la red exista.
