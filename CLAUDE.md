# SDLC Agent Pipeline

Este repositorio implementa un pipeline SDLC automatizado que va desde un ticket de Jira
hasta un Pull Request en GitHub usando agentes de IA especializados.

TEmperatura del Agente principal es 0.0

## Configuración

- Jira: conectado via MCP de Atlassian, Nombre proyecto `AI AGents`, clave de proyecto `AITEST`
- GitHub: conectado via MCP de GitHub, repositorios `https://github.com/johnjqc/ai-agents-autonomous-sdlc-platform`
- spec-kit: CLI local para generación de SDD
- Artefactos: se guardan en artifacts/

## Convenciones

- Los IDs de tickets siguen el formato PROJ-123
- Las ramas se crean con el patrón: feature/PROJ-123-titulo-corto
- Los PRs se abren siempre como draft
- El estado del pipeline se persiste en pipeline_state.json

## Flujo del pipeline

1. Agente Jira en `.claude/agents/jira-reader.md` lee el ticket via MCP de Atlassian
2. Agente SDD en `.claude/agents/spect-runner.md` genera el documento de diseño con spec-kit
4. Agente PR abre en `.claude/agents/cicd-runner.md` el Pull Request via MCP de GitHub


## Reglas de ejecucion

- Siempre usa los agentes para la ejecucion de cada step, nuca actues de forma autonoma
- Respeta el flujo del pipeli y valida la correcta ejecucion de cada etapa
- No inventes el proceso
- Valida que los agentes definidos existan de lo contrario ejecuta solo los agentes que existen
- Nunca crees archivo de agentes faltantes