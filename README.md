# SDLC Agent Pipeline — MVP con MCP

> Equipo de agentes de IA construido sobre **Claude Code** que automatiza el ciclo completo de desarrollo de software: desde la lectura de un ticket en **Jira** hasta la apertura de un **Pull Request en GitHub**. Toda comunicación con sistemas externos se realiza exclusivamente a través de servidores **MCP (Model Context Protocol)**, eliminando la necesidad de clientes REST ad-hoc.

---

## Visión general

El pipeline orquesta agentes especializados en secuencia. Cada agente recibe el contexto del anterior, lo enriquece y lo transfiere al siguiente. Las integraciones externas (Jira y GitHub) se abstraen como herramientas MCP que Claude Code puede invocar de forma nativa, igual que cualquier otra herramienta de su entorno.

```
Jira Cloud ──► [Atlassian MCP] ──► Jira Reader
                                        │ IssueData
                                        ▼
                         spec-kit ──► Agente SDD ──► SDD Document
                                        │
                                        ▼
                         [GitHub MCP] ◄── Agente PR ──► Pull Request
```

---

## Objetivos del MVP

- Leer un ticket de Jira (historia, criterios de aceptación, épica) usando el servidor MCP de Atlassian, sin llamadas REST directas.
- Crear el codigo con  **SDD** estructurado con **spec-kit**.
- Producir la implementación de código y tests básicos usando **Claude Code** como motor de generación.
- Crear una rama y abrir un **Pull Request en GitHub** usando el servidor MCP de GitHub, con descripción trazable al ticket y al SDD.

---

## Arquitectura

### Capa MCP

Toda comunicación con sistemas externos se enruta a través de servidores MCP registrados en el entorno de Claude Code. Los agentes nunca llaman APIs directamente o comando de consola: invocan herramientas MCP como si fueran funciones locales.

**Atlassian MCP** (`[jira-insights-mcp](https://github.com/aaronsb/jira-insights-mcp)`)
Expone herramientas para leer tickets, buscar issues con JQL, obtener épicas y metadatos de proyectos. Se autentica con el token de Atlassian del entorno. Ya disponible como conector en Claude.ai.

**GitHub MCP** (`@modelcontextprotocol/server-github`) 
Expone herramientas para crear ramas, hacer commits, abrir pull requests, añadir etiquetas y asignar revisores. Se autentica con un token de GitHub con permisos de escritura sobre el repositorio objetivo.

**spec-kit** (CLI local o Skills de Claude)
No es un servidor MCP remoto, sino una herramienta CLI local que el Agente SDD invoca directamente.

### Orquestador

Proceso central coordina los agentes en secuencia, gestiona el estado compartido entre ellos y maneja errores con reintentos configurables.

### Agentes

**Agente Jira**
Invoca herramientas del Atlassian MCP para descargar el ticket indicado. Extrae los datos y devuelve un objeto `IssueData` tipado.

**Agente SDD**
Recibe el `IssueData` y ejecuta `spec-kit` skills. Claude actúa como co-autor del documento, razonando sobre las decisiones técnicas a partir del contexto del ticket.

**Agente Coder**
Lee el `SDDDocument` e invoca Claude Code en el repositorio objetivo. Claude Code tiene acceso completo al sistema de archivos del repo: lee el código existente, identifica convenciones del proyecto y genera los archivos de implementación y tests descritos en el SDD. Devuelve la lista de archivos modificados.

**Agente PR**
Usa herramientas del GitHub MCP para crear una rama con nombre derivado del ID del ticket, hacer commit de los archivos generados y abrir el PR. La descripción del PR incluye enlace al ticket de Jira, resumen del SDD y checklist de revisión automatizado. El PR se abre siempre como **draft**.

---

## Stack tecnológico

| Componente | Tecnología |
|---|---|
| Motor de IA | ministral via ollama cloud |
| Ejecución de agentes | Claude Code CLI |
| Integración Jira | Atlassian MCP |
| Integración GitHub | GitHub MCP |
| Diseño de software | spec-kit |
| Configuración | `.env` |

---

## Variables de entorno

Copia `.env.example` a `.env`:

```env
# Atlassian (para el MCP server)
ATLASSIAN_TOKEN=...

# GitHub (para el MCP server)
GITHUB_TOKEN=ghp_...

# Anthropic
ANTHROPIC_API_KEY=sk-ant-...

```

---

## Flujo de ejecución detallado

**Paso 1 — Lectura del ticket (Agente Jira)**
El orquestador recibe `ISSUE_ID` (p. ej. `PROJ-142`). El Agente Jira invoca la herramienta Atlassian MCP. El resultado se parsea en un objeto `IssueData` tipado y se almacena en el estado compartido.

**Paso 2 — Generación del SDD (Agente SDD)**
El Agente SDD recibe el `IssueData`. Ejecuta el flujo basico `spec-kit` .

**Paso 3 — Apertura del PR (Agente PR)**
El Agente PR invoca las herramientas del GitHub MCP en secuencia: `createBranch` con nombre `feature/PROJ-142-short-title`, `createCommit` con los archivos generados, `createPullRequest` con descripción estructurada. El PR incluye enlace al ticket de Jira, sumario del SDD, lista de archivos modificados y checklist de revisión. Se abre como **draft**.

---

## Alcance del MVP y limitaciones

El MVP procesa tickets de tipo **historia de usuario** con criterios de aceptación definidos en texto plano. No cubre: tickets sin descripción, épicas, bugs con stack trace, o proyectos con tests de integración complejos.

El PR se abre siempre en modo **draft** como señal explícita de que el contenido fue generado por IA y requiere revisión humana antes del merge.
