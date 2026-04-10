# Recommended Figma Skills

## 1. figma-bmad-design-system-rules

### Objetivo

Convertir las decisiones de sistema visual y de componentizacion en reglas cortas, accionables y reutilizables para trabajar dentro de un archivo Figma que ya tiene libreria, estilos, variables o componentes existentes.

### Inputs esperados

- Libreria o design system existente
- Tokens/variables disponibles
- Reglas visuales conocidas del proyecto
- Lista de componentes base disponibles
- Restricciones de accesibilidad relevantes

### Output esperado

- Un bloque de reglas explicitas para usar el sistema existente
- Decision sobre que reutilizar, que extender y que no tocar
- Reglas de tokens/variables, naming, variants, states y exceptions

### Que partes de BMAD la alimentan

- `bmad-create-ux-design/steps/step-06-design-system.md`
- `bmad-create-ux-design/steps/step-08-visual-foundation.md`
- `bmad-create-ux-design/steps/step-11-component-strategy.md`
- `bmad-create-ux-design/steps/step-12-ux-patterns.md`
- `bmad-create-ux-design/steps/step-13-responsive-accessibility.md`
- `bmad-generate-project-context/project-context-template.md`
- `bmad-generate-project-context/steps/step-02-generate.md`
- `bmad-generate-project-context/steps/step-03-complete.md`

### Que secciones del material analizado deberian incorporarse al futuro SKILL.md

- Criterio para elegir entre sistema existente, sistema themeable o customizacion puntual.
- Semantic color mapping.
- Typography scale y spacing/grid foundation.
- Gap analysis entre componentes disponibles y necesidades reales.
- Especificacion minima por componente: purpose, anatomy, states, variants, accessibility.
- Reglas de patrones recurrentes: buttons, forms, navigation, feedback, loading, empty states.
- Breakpoints, contraste y touch target minimos.
- Formato compacto tipo `project-context`: reglas criticas, anti-patrones, don't-miss rules.

### Que cosas NO deberian entrar en esa skill

- Persona del agente.
- Investigacion emocional abierta.
- Exploracion larga de inspiracion.
- Menus A/P/C y protocolos BMAD.
- Detalles de PRD, arquitectura backend o deployment.
- Produccion de HTML visualizers.

## 2. figma-bmad-compose-screen

### Objetivo

Componer una pantalla o un flujo corto a partir de requerimientos existentes y de una libreria/sistema ya definido, priorizando jerarquia, patron correcto, estados y consistencia visual.

### Inputs esperados

- Objetivo de la pantalla
- FR o capability area relevante
- Journey o flujo de usuario asociado
- Sistema/libreria disponible
- Restricciones de plataforma y breakpoint
- Estados requeridos: empty, loading, error, success, disabled, etc.

### Output esperado

- Estructura de pantalla clara
- Lista de componentes a reutilizar
- Lista de componentes o variantes nuevas, si hacen falta
- Justificacion breve de jerarquia, navegacion y estados

### Que partes de BMAD la alimentan

- `bmad-create-ux-design/steps/step-02-discovery.md`
- `bmad-create-ux-design/steps/step-03-core-experience.md`
- `bmad-create-ux-design/steps/step-05-inspiration.md`
- `bmad-create-ux-design/steps/step-07-defining-experience.md`
- `bmad-create-ux-design/steps/step-09-design-directions.md`
- `bmad-create-ux-design/steps/step-10-user-journeys.md`
- `bmad-create-ux-design/steps/step-11-component-strategy.md`
- `bmad-create-prd/steps-c/step-04-journeys.md`
- `bmad-create-prd/steps-c/step-09-functional.md`

### Que secciones del material analizado deberian incorporarse al futuro SKILL.md

- Resumen del problema, usuario y core action antes de componer.
- Identificacion de la interaccion definitoria de la pantalla.
- Mental model del usuario.
- Success criteria visibles en la UI.
- Journey patterns y error recovery.
- Extraccion de patrones/anti-patrones de referencia.
- Gap analysis contra la libreria existente.
- Regla de no diseñar capacidades fuera del capability contract.

### Que cosas NO deberian entrar en esa skill

- Redaccion completa de PRD.
- Scope, vision o estrategia de producto general.
- Exploracion visual abierta de 6-8 direcciones.
- Arquitectura tecnica profunda.
- Reglas de commit, branches o testing de backend.

## 3. figma-bmad-handoff-readiness

### Objetivo

Validar que una pantalla, componente o flujo de Figma esta listo para handoff, con cobertura suficiente de estados, variantes, accesibilidad y consistencia con implementacion esperada.

### Inputs esperados

- Pantalla o flujo ya compuesto
- Lista de FR/NFR relevantes
- Reglas de naming/structure acordadas con desarrollo
- Tokens/variables y componentes usados
- Reglas de accesibilidad y responsive

### Output esperado

- Checklist de readiness con hallazgos concretos
- Lista de gaps de handoff
- Confirmacion de que esta cubierto y que falta
- Recomendaciones puntuales antes de entregar a desarrollo

### Que partes de BMAD la alimentan

- `bmad-create-ux-design/steps/step-11-component-strategy.md`
- `bmad-create-ux-design/steps/step-12-ux-patterns.md`
- `bmad-create-ux-design/steps/step-13-responsive-accessibility.md`
- `bmad-create-prd/data/prd-purpose.md`
- `bmad-create-prd/steps-c/step-09-functional.md`
- `bmad-create-prd/steps-c/step-10-nonfunctional.md`
- `bmad-create-prd/steps-c/step-11-polish.md`
- `bmad-create-architecture/steps/step-05-patterns.md`
- `bmad-create-architecture/steps/step-06-structure.md`
- `bmad-create-architecture/steps/step-07-validation.md`

### Que secciones del material analizado deberian incorporarse al futuro SKILL.md

- Validacion contra capability contract.
- Cobertura de estados y variantes.
- Reglas de naming y consistencia diseño-implementacion.
- Feedback/error/loading patterns.
- Responsive strategy y breakpoint checks.
- WCAG/contrast/touch targets/keyboard considerations.
- Mapeo entre feature/screen/component y boundary tecnica cuando aplique.
- Revision de requisitos blandos que suelen perderse en el polish.

### Que cosas NO deberian entrar en esa skill

- Decisiones de infraestructura, hosting o CI/CD.
- Versionado tecnico detallado salvo si afecta handoff.
- Exploracion de producto o descubrimiento inicial.
- Persona del agente y menus BMAD.
- Generacion de documentacion extensa no accionable.

## Recomendacion de adopcion

Implementar primero `figma-bmad-design-system-rules` y `figma-bmad-compose-screen`. `figma-bmad-handoff-readiness` deberia venir inmediatamente despues para cerrar el ciclo diseño -> consistencia -> entrega a desarrollo.
