# OSINT — Repo unificado

Todo el conocimiento OSINT en un solo lugar: documentación, catálogo de herramientas,
metodologías, OPSEC, verticales especializadas, recursos y la configuración de la VM dedicada.

## Estructura

```
osint/
├── 01-fundamentos/   # ciclo OSINT, Berkeley Protocol, ACH, cadena de custodia
├── 02-herramientas/  # ranking general, apps descargables, CLI
├── 03-tecnicas/      # verificación, falsos positivos, deepfakes, IA/LLM
├── 04-opsec/         # anonimato, extensiones, dark web, cripto, secretos
├── 05-especializado/ # GEOINT, financiero, telefonía, email, aéreo/marítimo, redes, CTI
├── 06-recursos/      # awesome lists, MCP servers, agentes, LLMs locales
├── 07-legal/         # política de uso, RGPD, cadena de custodia
└── vm/               # configuración y scripts de la VM OSINT
    ├── 00-docs/      # arquitectura y decisión de distro
    ├── 01-scripts/   # instalación, hardening, backup
    ├── 02-configs/   # dotfiles y configuraciones
    ├── 03-templates/ # plantillas Obsidian
    ├── 04-inventario/# catálogo de herramientas
    └── 05-legal/     # política de uso
```

## Base recomendada
Trace Labs OSINT VM 2026.10 (Debian 13) + BlackArch aislada + Obsidian como cuaderno enlazado.

## Seguridad
**No se suben** datos de investigación, credenciales, dumps, API keys ni PII (ver `.gitignore`).

## Relación con Obsidian
El cuaderno de trabajo vive en la bóveda `IA Brain` (notas `OSINT-*` enlazadas desde el Mapa Mental).