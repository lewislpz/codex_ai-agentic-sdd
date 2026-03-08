# codex_ai-agentic-sdd

Idioma / Language: [Español](README.es.md) | [English](README.en.md)

Plantilla de orquestación para desarrollo asistido por Codex con un flujo de trabajo guiado, verificable y orientado a documentación viva.

## ¿Qué hace este repositorio?
Este repositorio no es una aplicación final; define un **modelo operativo** para que agentes y desarrolladores trabajen con reglas claras durante todo el ciclo de entrega:

- planificación (`think`)
- implementación (`forge`)
- validación (`test`)
- revisión (`audit`)
- entrega (`ship` / `pr`)

La lógica principal está en documentación y contratos de trabajo dentro de `docs/` y `.codex/`.

## Utilidad práctica
Sirve para estandarizar cómo se trabaja con IA en repositorios reales, reduciendo ambigüedad y mejorando trazabilidad:

- define responsabilidades por fase y por rol
- centraliza políticas y prompts reutilizables
- fuerza validaciones antes de publicar cambios
- ayuda a mantener documentación y código alineados

Es útil como base para equipos que quieran un proceso repetible de desarrollo agentic sin depender de un stack específico (frontend/backend).

## Estructura clave
- `docs/`: contratos del repositorio (arquitectura, comandos, seguridad, stack)
- `.codex/policies/`: invariantes y reglas estables
- `.codex/prompts/`: entradas por fase
- `.codex/roles/`: responsabilidades por rol
- `.codex/knowledge/`: heurísticas y buenas prácticas reutilizables

## Flujo recomendado
1. Ejecutar `/think` para generar plan.
2. Implementar con `/forge execute` en rama de feature.
3. Verificar con `/test` (o comandos de validación del repo).
4. Revisar y entregar con `/ship` o `/pr`.

## Estado del proyecto
Template activo y agnóstico de stack, pensado para adaptarse a repositorios de producto sin imponer framework.
