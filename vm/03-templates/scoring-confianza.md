---
origen: opencode
creado: 2026-11-26
etiquetas: [osint, scoring, falsos-positivos]
---

# Scoring de Confianza

## Resumen
Sistema simple para puntuar la fiabilidad de un hallazgo y reducir falsos positivos.

## Contenido

| Nivel | Criterio |
|-------|----------|
| **Alta** | Confirmado por 2+ fuentes independientes + evidencia preservada (hash/Wayback). |
| **Media** | Una fuente sólida + indicios, pendiente de corroborar. |
| **Baja** | Una sola fuente no verificada o posible soft-404. |
| **Descartado** | Contradicho o confirmado como falso positivo. |

## Reglas
- Un "encontrado" en Sherlock/Maigret NO prueba propiedad → verificar abriendo el perfil.
- Registrar siempre la fuente y la fecha.
- No marcar "Alta" sin evidencia preservada.
- Revisar backlinks y contradicciones antes de cerrar.

## Relacionados
- [[Mapa Mental]]
- [[Plantilla-Nota]]