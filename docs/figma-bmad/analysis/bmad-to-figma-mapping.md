# BMAD to Figma Mapping

## Resumen ejecutivo

De los 5 elementos revisados, el mayor valor portable para Figma está en `bmad-create-ux-design`, seguido por fragmentos puntuales de `bmad-create-prd`, `bmad-create-architecture` y `bmad-generate-project-context`. `bmad-agent-ux-designer` aporta casi solo framing/persona y muy poca lógica reutilizable.

La recomendación práctica es no trasladar workflows BMAD completos a Figma Skills. Conviene extraer reglas operativas y convertirlas en skills cortas, secuenciales y centradas en: `design system rules`, `compose screen from existing system` y `handoff readiness`.

## 1. bmad-ux-designer

Nota: no se encontró un directorio con ese nombre exacto. El equivalente hallado es `bmad-agent-ux-designer`.

### Archivo(s) encontrados

- `bmad-agent-ux-designer/SKILL.md`
- `bmad-agent-ux-designer/bmad-skill-manifest.yaml`

### Propósito

Actuar como puerta de entrada/persona de UX Designer ("Sally"), cargar configuración y contexto del proyecto, presentar capacidades y enrutar al skill `bmad-create-ux-design`.

### Inputs

- Config BMAD (`_bmad/bmm/config.yaml`)
- `project-context.md` si existe
- Selección explícita del usuario

### Outputs

- Sesión/persona activa
- Tabla de capacidades
- Invocación de `bmad-create-ux-design`

### Pasos internos

1. Cargar config y resolver variables de idioma/paths.
2. Buscar `project-context.md`.
3. Saludar y presentar capacidades.
4. Esperar selección.
5. Invocar skill exacta sin inventar capacidades.

### Reglas de calidad o criterios

- Mantener personaje activo.
- No ejecutar menús automáticamente.
- No inventar capacidades.
- Invocar skills por nombre exacto.

### Artefactos que produce

- Ninguno persistente.

### Aportes al contexto Figma

Muy limitado. Lo rescatable no es la persona sino la idea de usar un contexto previo del proyecto antes de diseñar.

### [PORTAR]

- Cargar un contexto previo del proyecto antes de ejecutar una skill de Figma.

### [RESUMIR]

- Principios del rol UX: foco en necesidades reales, simplicidad inicial, atención a edge cases.

### [OMITIR]

- Persona "Sally".
- Saludo, tono, tabla de capacidades.
- Lógica de menú y routing BMAD.
- Dependencia de config BMAD.

### Conclusión breve de prioridad/valor

Prioridad baja. Sirve más como referencia de activación que como fuente de reglas útiles para Figma.

## 2. bmad-create-ux-design

### Archivo(s) encontrados

- `bmad-create-ux-design/SKILL.md`
- `bmad-create-ux-design/workflow.md`
- `bmad-create-ux-design/ux-design-template.md`
- `bmad-create-ux-design/steps/step-01-init.md`
- `bmad-create-ux-design/steps/step-02-discovery.md`
- `bmad-create-ux-design/steps/step-03-core-experience.md`
- `bmad-create-ux-design/steps/step-04-emotional-response.md`
- `bmad-create-ux-design/steps/step-05-inspiration.md`
- `bmad-create-ux-design/steps/step-06-design-system.md`
- `bmad-create-ux-design/steps/step-07-defining-experience.md`
- `bmad-create-ux-design/steps/step-08-visual-foundation.md`
- `bmad-create-ux-design/steps/step-09-design-directions.md`
- `bmad-create-ux-design/steps/step-10-user-journeys.md`
- `bmad-create-ux-design/steps/step-11-component-strategy.md`
- `bmad-create-ux-design/steps/step-12-ux-patterns.md`
- `bmad-create-ux-design/steps/step-13-responsive-accessibility.md`
- `bmad-create-ux-design/steps/step-14-complete.md`

### Propósito

Construir una especificación UX completa mediante un workflow colaborativo paso a paso, desde entendimiento del producto hasta patrones, componentes, responsive y accesibilidad.

### Inputs

- PRD, brief, documentación de proyecto, `project-context.md`
- Decisiones del usuario
- Guidelines de marca o paleta existente
- Apps de referencia e inspiración
- Decisiones sobre design system/plataforma

### Outputs

- `ux-design-specification.md`
- `ux-color-themes.html` esperado en el cierre
- `ux-design-directions.html` esperado en el cierre

### Pasos internos

1. Descubrir contexto y crear documento base.
2. Entender proyecto, usuarios, retos y oportunidades.
3. Definir experiencia central y plataforma.
4. Definir respuesta emocional deseada.
5. Analizar patrones e inspiración.
6. Elegir base de design system.
7. Definir interacción central y mecánica de éxito.
8. Establecer color, tipografía, spacing y layout.
9. Explorar direcciones visuales.
10. Diseñar user journeys y patrones de flujo.
11. Definir estrategia de componentes y gaps vs sistema base.
12. Documentar patrones de consistencia.
13. Definir responsive y accesibilidad.
14. Validar cierre y próximos pasos.

### Reglas de calidad o criterios

- Trabajo secuencial y colaborativo.
- No asumir; confirmar decisiones.
- Mantener consistencia con documentos previos.
- Documentar rationale.
- Considerar accesibilidad.
- Extraer patrones reutilizables.
- Diferenciar componentes del sistema vs custom.
- Identificar estados, variantes y comportamiento.

### Artefactos que produce

- Especificación UX integral.
- Visualizadores HTML para temas y direcciones visuales.

### Aportes al contexto Figma

Es la fuente más valiosa para futuras Figma Skills. Tiene contenido directamente transferible a reglas de system use, composición de pantallas, componentización, variantes, patrones y validación de responsive/a11y.

### [PORTAR]

- `step-06-design-system.md`: elección y adaptación de un sistema existente como base.
- `step-08-visual-foundation.md`: color system, semantic mapping, typography, spacing, grid y layout principles.
- `step-10-user-journeys.md`: conversión de journeys en flows y patrones repetibles.
- `step-11-component-strategy.md`: gap analysis entre sistema base y componentes custom; propósito, anatomía, estados, variantes y accesibilidad.
- `step-12-ux-patterns.md`: reglas reutilizables para botones, forms, navigation, feedback, loading, empty states y search/filter.
- `step-13-responsive-accessibility.md`: breakpoints, touch targets, contrast, keyboard/screen reader checks y testing checklist.
- `step-07-defining-experience.md`: definición de la interacción central, mental model, success criteria y mechanics.

### [RESUMIR]

- `step-02-discovery.md`: resumen de visión, usuarios, retos y oportunidades como contexto de diseño.
- `step-03-core-experience.md`: principios de experiencia y momentos críticos.
- `step-04-emotional-response.md`: solo si se traduce a decisiones visuales/interaction tone concretas.
- `step-05-inspiration.md`: usar como extracción de patrones/anti-patrones, no como research abierto.
- `step-09-design-directions.md`: conservar la idea de comparar direcciones, pero no el mecanismo HTML ni la exploración demasiado amplia.
- `workflow.md` y `ux-design-template.md`: solo como estructura macro, no como skill futura literal.

### [OMITIR]

- Menús A/P/C.
- Llamadas a `bmad-advanced-elicitation` y `bmad-party-mode`.
- Frontmatter y tracking de `stepsCompleted`.
- Cierre de workflow y actualización de status.
- Dependencias de config BMAD y lenguaje de agente.
- Generación de assets HTML como requisito estructural.

### Conclusión breve de prioridad/valor

Prioridad máxima. Aquí está casi todo lo que conviene convertir en skills Figma pequeñas y orientadas a ejecución.

## 3. bmad-create-prd

### Archivo(s) encontrados

- `bmad-create-prd/SKILL.md`
- `bmad-create-prd/workflow.md`
- `bmad-create-prd/templates/prd-template.md`
- `bmad-create-prd/data/prd-purpose.md`
- `bmad-create-prd/steps-c/step-01-init.md`
- `bmad-create-prd/steps-c/step-04-journeys.md`
- `bmad-create-prd/steps-c/step-09-functional.md`
- `bmad-create-prd/steps-c/step-10-nonfunctional.md`
- `bmad-create-prd/steps-c/step-11-polish.md`

### Propósito

Crear un PRD denso, trazable y consumible tanto por humanos como por artefactos downstream de BMAD.

### Inputs

- Briefs
- Research
- Brainstorming
- Documentación existente
- Contexto de proyecto
- Conversación con el usuario

### Outputs

- `prd.md`

### Pasos internos

1. Inicializar y descubrir contexto.
2. Descubrir visión y alcance.
3. Mapear user journeys.
4. Definir requisitos funcionales.
5. Definir NFR relevantes.
6. Pulir para densidad, trazabilidad y coherencia.

### Reglas de calidad o criterios

- Alta densidad informativa.
- Trazabilidad desde visión a journeys y requirements.
- FR = capacidad, no implementación.
- NFR = medible y relevante.
- Evitar adjetivos vagos, leakage técnico y fluff.
- Cubrir accesibilidad/compliance cuando aplique.

### Artefactos que produce

- PRD estructurado en Markdown.

### Aportes al contexto Figma

No es una skill de diseño, pero sí aporta un upstream útil para componer pantallas y validar handoff. Lo más valioso es la relación `journeys -> capabilities -> NFR`.

### [PORTAR]

- `step-04-journeys.md`: cobertura de user types, success path, edge cases y journeys secundarios que luego implican pantallas/estados.
- `step-09-functional.md`: usar FR como contrato de capacidades para no diseñar features no especificadas.
- `step-10-nonfunctional.md`: accesibilidad y otros NFR relevantes como criterios de handoff/readiness.

### [RESUMIR]

- `data/prd-purpose.md`: principios de densidad informativa, trazabilidad y lenguaje medible.
- `step-11-polish.md`: reconciliación de ideas blandas y chequeo de coherencia antes del handoff.
- `workflow.md` y `step-01-init.md`: detección de inputs útiles para el diseño, sin conservar la mecánica completa.

### [OMITIR]

- Executive summary, vision, scope y PM facilitation como skill Figma.
- Domain requirements no relacionados con UI/UX.
- Project-type requirements puramente técnicos.
- Menús/protocolos BMAD y append-only workflow.

### Conclusión breve de prioridad/valor

Prioridad media. No debe convertirse en skill Figma, pero sí alimentar reglas de composición y checklist de handoff.

## 4. bmad-create-architecture

### Archivo(s) encontrados

- `bmad-create-architecture/SKILL.md`
- `bmad-create-architecture/workflow.md`
- `bmad-create-architecture/architecture-decision-template.md`
- `bmad-create-architecture/steps/step-01-init.md`
- `bmad-create-architecture/steps/step-02-context.md`
- `bmad-create-architecture/steps/step-04-decisions.md`
- `bmad-create-architecture/steps/step-05-patterns.md`
- `bmad-create-architecture/steps/step-06-structure.md`
- `bmad-create-architecture/steps/step-07-validation.md`

### Propósito

Tomar decisiones de arquitectura y fijar patrones de implementación para que múltiples agentes implementen de forma consistente.

### Inputs

- PRD obligatorio
- UX spec si existe
- Research y project docs
- Project context
- Decisiones del usuario

### Outputs

- `architecture.md`

### Pasos internos

1. Inicializar y validar inputs.
2. Analizar implicaciones arquitectónicas del PRD/UX.
3. Tomar decisiones core.
4. Definir patrones y reglas de consistencia.
5. Mapear estructura y boundaries.
6. Validar cobertura y readiness.

### Reglas de calidad o criterios

- Coherencia entre decisiones.
- Cobertura de FR/NFR.
- Patrones explícitos para evitar divergencia entre agentes.
- Estructura concreta, no genérica.
- Validación de readiness antes de implementar.

### Artefactos que produce

- Documento de decisiones arquitectónicas.

### Aportes al contexto Figma

No aporta UI directa, pero sí material muy útil para `design-implementation consistency` y `handoff`. En particular, las categorías de conflictos y la validación de cobertura pueden traducirse a checks de diseño-dev.

### [PORTAR]

- `step-05-patterns.md`: naming, structure, format, error/loading/state patterns como contrato con desarrollo.
- `step-07-validation.md`: validación de cobertura FR/NFR, completitud y readiness para handoff.

### [RESUMIR]

- `step-02-context.md`: extraer implicaciones técnicas de UX como performance, responsive, a11y y real-time needs.
- `step-06-structure.md`: mapping de features/FR categories a módulos o boundaries para handoff.
- `architecture-decision-template.md`: solo como patrón de salida si se crea un checklist Figma-to-dev.

### [OMITIR]

- Starter templates.
- Decisiones de data architecture, infra, auth y deployment salvo si afectan directamente el handoff UI.
- Búsqueda de versiones web y stack decisions puramente técnicas.
- Frontmatter/status y mecánica de workflow.

### Conclusión breve de prioridad/valor

Prioridad media-alta para `handoff readiness`, baja para composición visual directa.

## 5. bmad-generate-project-context / project-context

### Archivo(s) encontrados

- `bmad-generate-project-context/SKILL.md`
- `bmad-generate-project-context/workflow.md`
- `bmad-generate-project-context/project-context-template.md`
- `bmad-generate-project-context/steps/step-01-discover.md`
- `bmad-generate-project-context/steps/step-02-generate.md`
- `bmad-generate-project-context/steps/step-03-complete.md`

No se encontró una skill separada llamada `project-context`; lo encontrado corresponde al generador y al template/output esperado.

### Propósito

Crear un `project-context.md` conciso con reglas críticas y no obvias para que agentes implementen con consistencia.

### Inputs

- `architecture.md`
- Archivos del proyecto (`package.json`, configs, tests, etc.)
- Código existente
- Contexto ya documentado si existe

### Outputs

- `project-context.md`

### Pasos internos

1. Descubrir stack, convenciones y reglas existentes.
2. Generar reglas por categorías.
3. Optimizar el documento para consumo LLM y completarlo con guías de uso.

### Reglas de calidad o criterios

- Mantener contenido lean y no obvio.
- Priorizar reglas accionables.
- Documentar versiones exactas cuando importan.
- Optimizar para escaneo rápido.
- Incluir anti-patrones y edge cases.

### Artefactos que produce

- `project-context.md`

### Aportes al contexto Figma

Muy útil como patrón de compresión: tomar reglas de diseño y convertirlas en un archivo corto de alto valor. El aporte no es el contenido técnico específico, sino la forma de empaquetar reglas críticas.

### [PORTAR]

- `project-context-template.md`: formato corto de reglas críticas.
- `step-02-generate.md`: estructura por categorías y énfasis en "critical don't-miss rules".
- `step-03-complete.md`: optimización para alta densidad y uso rápido por agentes.

### [RESUMIR]

- `step-01-discover.md`: descubrimiento de patrones existentes como insumo para reglas Figma.
- Secciones de stack/versions: convertirlas en librería base, sistema de componentes, tokens o convenciones del archivo Figma.
- Usage guidelines: adaptar a "cómo debe usarlo una skill de Figma".

### [OMITIR]

- Reglas de branches, commits, PRs y deployment.
- Reglas de lenguaje/framework puramente de código cuando no afecten handoff.
- Dependencia de package files y scanning técnico como fin en sí mismo.

### Conclusión breve de prioridad/valor

Prioridad media-alta como patrón de empaquetado. Es especialmente útil para una futura skill de reglas de sistema y para checklists de consistencia diseño-implementación.

## Variantes, duplicados y ausencias

- `bmad-ux-designer` no aparece con ese nombre exacto; el equivalente encontrado es `bmad-agent-ux-designer`.
- No se encontró una skill independiente llamada `project-context`; sí existe `bmad-generate-project-context` y el template/output `project-context.md`.
- No se observaron duplicados funcionales completos, pero sí superposición parcial entre:
  - `bmad-create-ux-design/steps/step-03-core-experience.md` y `step-07-defining-experience.md`
  - `bmad-create-architecture/step-05-patterns.md` y `bmad-generate-project-context/step-02-generate.md`

## Prioridad recomendada de extracción

1. `bmad-create-ux-design`
2. `bmad-generate-project-context`
3. `bmad-create-architecture`
4. `bmad-create-prd`
5. `bmad-agent-ux-designer`
