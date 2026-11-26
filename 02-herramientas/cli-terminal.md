# Informe OSINT — Mejores Herramientas de Terminal / CLI (2026)

> Investigación OSINT de código abierto para Linux / macOS / Windows (terminal).
> Fecha de referencia: noviembre 2026. Las cifras de "stars" son aproximadas y cambian con el tiempo.

---

## 1. Resumen: las 15 MEJORES herramientas de terminal OSINT

Ordenadas por utilidad / popularidad combinadas (adopción, mantenimiento y versatilidad):

| # | Herramienta | Categoría principal | Por qué destaca |
|---|-------------|---------------------|-----------------|
| 1 | **Sherlock** | Username | El estándar de facto; ~118k★, 400+ redes, un solo comando. |
| 2 | **Maigret** | Username (profundo) | Fork superlativo de Sherlock; 6K–10K sitios, extrae perfil, grafos y reportes PDF/HTML. ~41k★. |
| 3 | **BBOT** | Framework OSINT recursivo | Escáner modular "inspirado en SpiderFoot", 80+ módulos, ASM y bug bounty. ~11k★. |
| 4 | **theHarvester** | Emails / dominios / hosts | Recolector clásico de correos, subdominios y hosts; decenas de fuentes. |
| 5 | **SpiderFoot** | Framework all-in-one | Automatiza OSINT con cientos de módulos y correlación; interfaz web + CLI. |
| 6 | **Amass (OWASP)** | Recon de dominios | Mapeo de superficie de ataque en profundidad; estándar en inventario de activos. ~15.6k★. |
| 7 | **Subfinder** | Subdominios (pasivo) | El más rápido en enumeración pasiva; ideal para pipelines. 10k★+. |
| 8 | **Recon-ng** | Framework modular | Framework tipo Metasploit para OSINT, con marketplace de módulos. ~6.1k★. |
| 9 | **Holehe** | Email OSINT | Comprueba si un email está registrado en 120+ sitios vía "forgot password". |
| 10 | **ExifTool** | Metadatos | El referente absoluto para leer/escribir metadatos (GPS, dispositivo, fecha). |
| 11 | **WhatsMyName (CLI/wmn-data)** | Username (dataset) | Dataset de 691 sitios reutilizado por decenas de herramientas (archivado nov-2026). |
| 12 | **Instaloader** | Scraping Instagram | Scraper CLI más mantenido; descarga posts/stories/metadatos. ~13k★. |
| 13 | **Toutatis** | Instagram OSINT | Extrae emails/teléfonos públicos de perfiles de Instagram. ~4.5k★. |
| 14 | **vt-cli / VirusTotal CLI** | Threat Intel | Enriquecimiento y búsqueda en VirusTotal desde terminal. |
| 15 | **Sublist3r** | Subdominios | Clásico veterano, rápido y sencillo (mantenimiento más lento). |

---

## 2. Tablas por categoría

### 2.1 OSINT de usernames y personas

| Herramienta | Instalación | Qué hace | Mantenimiento / Popularidad | Destaca por |
|-------------|-------------|----------|-----------------------------|-------------|
| **Sherlock** | `pipx install sherlock-project` / `pip install sherlock-project` / Docker `sherlock/sherlock` | Busca un username en 400+ redes y devuelve URLs de perfiles. | Muy activo (v0.16.0, 2026); ~117.8k★, 13.4k forks. | Rapidez, scriptable, salida TXT/CSV/XLSX/JSON. |
| **Maigret** | `pip3 install maigret` / `snap install maigret` / Docker `soxoj/maigret` | Dossier por username en 6K–10K sitios; parsea perfil, enlaces y hace búsqueda recursiva. | Muy activo (v0.6.6, sep-2026); ~41.3k★; 75k+ installs/mes. | Menor tasa de falsos positivos; reportes HTML/PDF/XMind/CSV/JSON; modo IA `--ai`. |
| **WhatsMyName** | Web (whatsmyname.app) o cliente CLI `wmnc.py` (Python) | Dataset `wmn-data.json` de 691 sitios para enumeración de cuentas. | **Archivado 9-nov-2026** (dataset final). Base de datos muy reutilizada. | Su JSON es el "sustrato" de detección de muchas herramientas. |
| **Holehe** | `git clone` + `python3 setup.py install` / Docker | Comprueba si un email está registrado en 120+ sitios usando el flujo de recuperación/contraseña. | Mantenimiento medio; proyecto popular (megadose). | Identificador = **email** (no username); complementa a Sherlock/Maigret. |

> Nota de la comparativa 2026 (Holehe vs Sherlock vs Maigret vs WhatsMyName): Sherlock ≈481 sitios, WhatsMyName ≈691 activos, Maigret ≈7.516 activos de 8.215 listados.

### 2.2 Reconocimiento de dominios / subdominios

| Herramienta | Instalación | Qué hace | Mantenimiento / Popularidad | Destaca por |
|-------------|-------------|----------|-----------------------------|-------------|
| **Subfinder** | `go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest` | Enumeración **pasiva** de subdominios desde múltiples fuentes. | Muy activo (v2.17.0, oct-2026); 10k★+ (superó 10k en 2024). | **El más rápido**; flags `-all`, `-recursive`, salida JSONL. |
| **Amass (OWASP)** | Binarios Go / `go install` / Docker / Snap | Mapeo de superficie de ataque y descubrimiento de activos en profundidad (passivo + activo). | Activo (actualizado oct-2026); ~15.6k★. | Cobertura profunda, correlación de activos, integración OWASP. |
| **Sublist3r** | `git clone` + `pip install -r requirements.txt` | Enumeración de subdominios vía motores y APIs (crt.sh, VirusTotal, etc.). | Mantenimiento lento; clásico muy conocido. | Sencillez; modo fuerza bruta `-b`. |
| **BBOT** (preset `subdomain-enum`) | `pipx install bbot` | Enumeración recursiva y modular; en benchmarks superó a otros en nº de subdominios. | Muy activo (rama stable nov-2026); ~11.2k★. | Recursividad + 80 módulos; preset `subdomain-enum`. |

### 2.3 Enumeración de infraestructura y emails

| Herramienta | Instalación | Qué hace | Mantenimiento / Popularidad | Destaca por |
|-------------|-------------|----------|-----------------------------|-------------|
| **theHarvester** | `git clone` + `uv sync` / `pip install theHarvester` | Recolecta emails, subdominios, hosts y nombres desde fuentes públicas. | Activo; proyecto veterano muy usado. | Ligero y eficiente; salida a múltiples formatos. |
| **Recon-ng** | `git clone` + `pip install -r REQUIREMENTS` → `./recon-ng` | Framework modular OSINT con base de datos y marketplace de módulos. | Mantenimiento intermitente; ~6.1k★. | Arquitectura tipo Metasploit; automatiza flujos con workspaces. |

### 2.4 Frameworks OSINT completos (all-in-one)

| Herramienta | Instalación | Qué hace | Mantenimiento / Popularidad | Destaca por |
|-------------|-------------|----------|-----------------------------|-------------|
| **SpiderFoot** | `git clone` + `python3 sf.py -l 127.0.0.1:5001` | Automatiza OSINT con cientos de módulos y correlación de resultados. | Proyecto maduro; interfaz web + CLI (`sfcli.py`). | Cobertura enorme; correlación automática; mapas de datos. |
| **BBOT** | `pipx install bbot` / Docker | Escáner recursivo modular (recon, bug bounty, ASM). | Muy activo; ~11.2k★; 80+ módulos. | Diseño asíncrono, extensible como librería Python. |
| **Recon-ng** | (ver arriba) | Framework modular con marketplace. | ~6.1k★. | Estructura de "workspaces" y API REST. |

### 2.5 Análisis de metadatos

| Herramienta | Instalación | Qué hace | Mantenimiento / Popularidad | Destaca por |
|-------------|-------------|----------|-----------------------------|-------------|
| **ExifTool** | `apt install exiftool` / `brew install exiftool` / pkg macOS / .exe Windows | Lee, escribe y edita metadatos de imágenes, documentos y vídeo (GPS, cámara, fechas, autor). | Muy activo (v13.64, 2026); referente de la industria. | Soporta cientos de formatos; procesamiento por lotes a CSV/JSON (`exiftool -r -json ./dir`). |

### 2.6 OSINT de redes sociales / scraping

| Herramienta | Instalación | Qué hace | Mantenimiento / Popularidad | Destaca por |
|-------------|-------------|----------|-----------------------------|-------------|
| **Instaloader** | `pip install instaloader` | Descarga posts, stories, metadatos y perfiles públicos de Instagram. | Muy activo (v4.15.3, jul-2026); ~13.1k★. | Scraper CLI de Instagram más mantenido. |
| **Toutatis** | `pip install toutatis` | Extrae emails/teléfonos y datos públicos de cuentas de Instagram. | Activo; ~4.5k★. | OSINT de perfil (no archivo de posts). |
| **Osintgram** | `git clone` + `pip install -r requirements` | CLI interactivo para análisis de perfiles y redes de seguidores. | Mantenimiento medio. | Mapeo de red de seguidores. |
| **TWINT** | `pip install twint` | Scraping avanzado de Twitter/X sin API oficial. | **Uso degradado** tras cambios de X; histórico. | Precursor de scraping Twitter sin API. |
| **xint** | CLI (Rust/Node) | Busca, monitoriza y exporta datos públicos de X para investigación. | Emergente (2026). | Alternativa moderna a TWINT. |

### 2.7 Threat Intelligence CLI

| Herramienta | Instalación | Qué hace | Mantenimiento / Popularidad | Destaca por |
|-------------|-------------|----------|-----------------------------|-------------|
| **vt-cli (VirusTotal)** | `pip install vt-py` / binarios oficiales | Búsqueda y enriquecimiento de hashes, dominios, IPs y URLs en VT Intelligence. | Oficial, activo (2026). | Integración oficial con la API de VirusTotal. |
| **AbuseIPDB / urlscan CLI** | `pip install` (clientes de API) | Reputación de IP/URL y análisis de dominios. | Común en pipelines CTI. | Enriquecimiento rápido de indicadores. |

### 2.8 Google dorking automatizado

| Herramienta | Instalación | Qué hace | Mantenimiento / Popularidad | Destaca por |
|-------------|-------------|----------|-----------------------------|-------------|
| **dorks / dork generators** (varios) | `git clone` + Python | Genera y ejecuta dorks de Google/Bing automatizados para descubrir archivos y endpoints expuestos. | Proyectos comunitarios variables. | Automatiza operadores de búsqueda avanzada. |
| **theHarvester** (`-b google`) | (ver arriba) | Incluye módulo de búsqueda tipo dork para emails/hosts. | Activo. | Dorking integrado en recolección mayor. |

> Muchos "dorkers" son scripts pequeños; conviene combinarlos con frameworks (BBOT/Recon-ng) para orquestarlos.

---

## 3. Flujo de trabajo recomendado (ejemplo)

1. **Identidad**: `maigret usuario` (profundo) → `sherlock usuario` (rápido) → `holehe correo@dominio.com`.
2. **Dominio**: `subfinder -d dominio.com` → `amass enum -passive -d dominio.com` → `theHarvester -d dominio.com -b all`.
3. **Correlación / ASM**: `bbot -t dominio.com -f subdomain-enum web-basic` o SpiderFoot.
4. **Metadatos**: `exiftool -r -json ./descargas > metadata.json`.
5. **Redes**: `instaloader perfil` / `toutatis usuario`.
6. **CTI**: `vt-cli` sobre indicadores obtenidos.

---

## 4. Notas de uso responsable y legal

- **Legalidad**: el OSINT es, en sí, legal, pero *cómo* se usa marca la diferencia. Respeta **GDPR** (UE), **CCPA** (California), **CFAA** (EE. UU.) y la legislación local. No existe un estándar internacional único.
- **Base legal**: si procesas datos personales (aunque sean públicos), en la UE necesitas base jurídica y respetar minimización, finalidad y derechos del interesado (acceso, supresión).
- **Autorización**: para pentesting/ASM sobre activos que no te pertenecen, obtiene **autorización por escrito** (alcance, ventana temporal, reglas de enfrentamiento).
- **Privacidad**: no accedas a cuentas privadas, no eludas autenticación, no acoses ni hagas doxxing. La recolección pasiva de datos públicos es lo aceptable.
- **Scraping**: respeta `robots.txt`, términos de servicio y límites de tasa; el scraping agresivo puede ser ilegal o sancionable.
- **Documentación**: registra qué datos usas, de dónde y para qué (transparencia y rendición de cuentas).
- **Código de conducta**: define valores y límites antes de investigar; conserva los datos solo el tiempo necesario y elimínalos después.
- **Herramientas**: úsalas solo contra objetivos propios o autorizados y con fines educativos/defensivos.

---

## 5. Fuentes principales

- Sherlock — github.com/sherlock-project/sherlock (117.8k★) · Bellingcat Toolkit.
- Maigret — github.com/soxoj/maigret (41.3k★) · PyPI v0.6.6 (sep-2026).
- WhatsMyName — github.com/WebBreacher/WhatsMyName (archivado 9-nov-2026, 691 sitios).
- Holehe — github.com/megadose/holehe.
- Subfinder — github.com/projectdiscovery/subfinder (v2.17.0, oct-2026).
- OWASP Amass — github.com/owasp-amass/amass (15.6k★).
- Sublist3r — github.com/aboul3la/Sublist3r.
- theHarvester — github.com/laramies/theHarvester.
- Recon-ng — github.com/lanmaster53/recon-ng (6.1k★).
- SpiderFoot — github.com/smicallef/spiderfoot.
- BBOT — github.com/blacklanternsecurity/bbot (11.2k★).
- ExifTool — exiftool.org (v13.64).
- Instaloader — github.com/instaloader/instaloader (13.1k★, v4.15.3).
- Toutatis — github.com/megadose/toutatis (4.5k★).
- vt-cli — github.com/VirusTotal/vt-cli.
- Comparativas y legalidad: shadowdragon.io, maxintel.org, holehe.org, scrapfly.io, hensoldt.net, osint-central.com, mcafeeinstitute.edu.