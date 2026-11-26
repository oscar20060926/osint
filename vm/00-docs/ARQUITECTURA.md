# Arquitectura de la VM OSINT

## Objetivo
VM dedicada exclusivamente a OSINT, con Obsidian como cuaderno enlazado para detectar falsos positivos.

## Componentes
- **Base:** Trace Labs OSINT VM 2026.10 (Debian 13).
- **Cuaderno:** Obsidian (bóveda enlazada, plantillas, Dataview).
- **Herramientas extra:** BlackArch en VM/contenedores aparte.
- **Preservación:** Hunchly + Wayback Machine + Auto Archiver.
- **Secretos:** KeePassXC + volumen cifrado (fuera del repo).

## Aislamiento
- VM principal OSINT (sin herramientas ofensivas).
- VM BlackArch separada para recon/pentest.
- Snapshot (Timeshift) antes de cada investigación.

## Ver
- [[DECISION-DISTRO]]
- [[POLITICA-USO]]