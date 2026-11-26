# Informe OSINT 2026 — Técnicas y Metodologías para Complementar una VM de Investigación

> Investigador OSINT senior · Fecha de elaboración: noviembre 2026.
> Alcance: metodologías, verificación/anti-falsos-positivos, IA/LLM y agentes, automatización con Python, y preservación de evidencia/cadena de custodia.
> Nota de rigor: todo lo aquí expuesto procede de fuentes consultadas en 2025–2026. Cuando un dato no se pudo confirmar de forma independiente, se marca como *[no confirmado]* o *[a verificar]*. Las herramientas cambian de precio/funciones con frecuencia: verificar antes de depender de un detalle.

---

## 1. Metodologías y frameworks de investigación OSINT

### 1.1 Berkeley Protocol on Digital Open Source Investigations
- **Qué es:** Protocolo internacional (OHCHR + Human Rights Center, UC Berkeley) que fija **estándares mínimos profesionales** para identificar, recolectar, preservar, verificar y analizar información de fuente abierta digital, orientado a investigaciones de derecho penal internacional, DDHH y humanitarias. Publicado en inglés el 1 dic 2020; edición ONU en 2022 (6 idiomas, incl. español). Usado por fiscales ucranianos para documentar crímenes de guerra.
- **Tipo:** Gratis (PDF público).
- **Por qué sirve:** Es el marco de referencia global para que la evidencia OSINT sea **admisible y defendible** en tribunales. Define el **ciclo de investigación OSINT** en 6 pasos: (1) Online inquiries [búsqueda + monitoreo], (2) Preliminary assessment, (3) Collection, (4) Preservation, (5) Verification, (6) Investigative analysis. Introduce distinciones clave: *credibilidad* (confiabilidad), *fiabilidad* (consistencia), *veracidad/validez* (exactitud). Deriva la minimización de datos del GDPR.
- Fuentes: https://www.ohchr.org/en/publications/policy-and-methodological-publications/berkeley-protocol-digital-open-source · PDF: https://www.ohchr.org/sites/default/files/2022-04/OHCHR_BerkeleyProtocol.pdf · https://humanrights.berkeley.edu/projects/developing-the-berkeley-protocol-on-digital-open-source-investigations
- **Complemento legal:** *Evaluating Digital Open Source Imagery: A Guide for Judges and Fact-Finders* (Berkeley, may 2024) — guía para jueces/evaluadores: https://humanrights.berkeley.edu/wp-content/uploads/archive/2024/05/Guide-for-judges.pdf

### 1.2 Analysis of Competing Hypotheses (ACH)
- **Qué es:** Método analítico de **Richards J. Heuer Jr.** (veterano de la CIA, años 70) formalizado en *Psychology of Intelligence Analysis*. En lugar de buscar confirmación de la hipótesis favorita, se busca **refutar** hipótesis mediante una matriz evidencia × hipótesis.
- **Tipo:** Gratis (libro y método públicos); varias herramientas de software (algunas gratuitas, otras de pago).
- **Por qué sirve:** Reduce el **sesgo de confirmación** (clave para evitar falsos positivos en OSINT). Proceso de 8 pasos: (1) identificar todas las hipótesis (idealmente mutuamente excluyentes), (2) listar evidencia/argumentos a favor y en contra, (3) construir matriz, (4) refinar/eliminar evidencia no diagnóstica, (5) conclusiones tentativas buscando **desmentir**, (6) análisis de sensibilidad de evidencias críticas, (7) reportar según verosimilitud relativa, (8) hitos de observación futura. La hipótesis más probable es la que **menos evidencia en contra** tiene.
- Fuentes: https://www.cia.gov/resources/csi/static/Pyschology-of-Intelligence-Analysis.pdf · https://en.wikipedia.org/wiki/Analysis_of_competing_hypotheses · https://pherson.org/wp-content/uploads/2013/06/Improving-Intelligence-Analysis-with-ACH.pdf · NCSC (Países Bajos): https://www.ncsc.nl/analysetechnieken/analysis-of-competing-hypotheses-ach
- **Herramientas ACH:** PARC ACH 2.0 (con Heuer), ACH0 (PARC), Decision Command, DECIDE (SSS Research). Verificar disponibilidad actual *[a verificar]*.

### 1.3 Ciclo de Inteligencia / OSINT cycle
- **Qué es:** Marco de 5–6 fases para transformar datos brutos en inteligencia terminada. Variante estándar: **Planificación y dirección → Recolección → Procesamiento y explotación → Análisis y producción → Difusión** (+ *Retroalimentación/Evaluación* en el modelo de 6 pasos de Joint Publication 2.0).
- **Tipo:** Gratis (doctrina pública).
- **Por qué sirve:** Da estructura reproducible al trabajo; la fase de **planificación** se apoya en las **5W+H** (quién, qué, cuándo, dónde, por qué, cómo) y en OPSEC/archivado. La retroalimentación cierra el ciclo (una difusión suele generar nuevos requisitos).
- Fuentes: https://www.intelligence.gov/how-the-ic-works · https://www.fivecast.com/blog/osint-fundamentals-osint-the-intelligence-cycle · https://irp.fas.org/nsa/ioss/threat96/part02.htm · https://www.osintfoundation.com/images/osint/OSINT%20COLLECTION%20METHODOLOGIES.pdf

### 1.4 Reconocimiento en Cyber Kill Chain
- **Qué es:** La fase de **Reconnaissance** (recon) es la primera etapa del Cyber Kill Chain de Lockheed Martin (Recon → Weaponization → Delivery → Exploitation → Installation → C2 → Actions on Objectives). En OSINT defensivo/atribución se usa para mapear infraestructura del adversario.
- **Tipo:** Gratis (framework público).
- **Por qué sirve:** Aporta un modelo mental de **qué buscar** en la huella digital (dominios, IPs, certificados, correos, empleados expuestos) y conecta OSINT con threat intelligence. En OSINT ofensivo/red team, el recon es el paso inicial de enumeración pasiva.
- Fuente (marco): https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html *(URL corporativa; verificar)*. Reconocimiento OSINT aplicado: theHarvester, Amass, SpiderFoot (ver §4).

### 1.5 Marcos complementarios
- **SIFT** (Mike Caulfield) y **Lateral Reading** (Wineburg & McGrew, 2019): ver §2.
- **TCPED** (Tasking, Collection, Processing, Exploitation, Dissemination) — variante doctrinal de EE.UU. para OSINT; fuente OSINT Foundation.
- **ABCDE Framework** para análisis de desinformación (mencionado en el Best Practices Repository de Alliance4Europe, nov 2025): https://alliance4europe.eu/wp-content/uploads/2025/12/OSINT-Best-Practices-Repository-%E2%80%93-Alliance4Europe-%E2%80%93-November-2025.pdf

---

## 2. Verificación y detección de falsos positivos

Principio rector (Berkeley + práctica 2026): **ningún resultado de un detector automático es prueba de autenticidad**; la ausencia de detección no prueba que algo sea real, y la detección es probabilística y suele ir "una generación por detrás" de la generación de fakes.

### 2.1 Triangulación de fuentes y lectura lateral
- **Triangulación:** contrastar el mismo hecho en ≥3 fuentes independientes y fiables antes de darlo por bueno (regla práctica de fact-checking).
- **Lateral Reading:** no evaluar una fuente leyéndola "en vertical" (su propia página "About"), sino abrir pestañas y ver **qué dicen terceros** de esa fuente. Técnica de fact-checkers profesionales.
- **SIFT** (Stop, Investigate the source, Find better coverage, Trace claims/quotes/media to original context): método de 4 movimientos para evaluar en línea; integra lateral reading y "trace al origen".
- **Tipo:** Gratis (metodologías).
- **Por qué sirven:** Atacan directamente el falso positivo por **fuente sesgada o descontextualizada**; "trace al contexto original" evita aceptar citas/imágenes fuera de contexto.
- Fuentes: https://guides.lib.uw.edu/research/evaluate/sift · https://libguides.princeton.edu/medialiteracy/lateralreading · https://mediahelpingmedia.org/basics/sift-for-fact-checking/ · https://pressbooks.pub/webliteracy/chapter/what-reading-laterally-means/

### 2.2 Reverse Image Search (búsqueda inversa de imágenes)
Herramientas clave (usar **al menos dos** motores; un acierto en Yandex y no en Google suele indicar origen ruso/europeo oriental):

| Herramienta | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| **Google Lens / Google Images** | Coincidencia visual + búsqueda semántica; vista "Exact matches" | Gratis | Mayor cobertura; contexto "About this image" y etiquetas C2PA |
| **Yandex Images** | Búsqueda inversa, fuerte en zonas de conflicto y web rusa | Gratis | Encuentra imágenes que los motores occidentales no ven |
| **TinEye** | Indexa por contenido; ordena por aparición **más antigua** | Gratis (API de pago) | Ideal para detectar la instancia original y reutilizaciones |
| **Bing Visual Search** | Cobertura alternativa | Gratis | Segundo índice para contraste |
| **InVID-WeVerify** | Extrae keyframes de vídeo y los busca en varios motores a la vez | Gratis | Verificación de vídeo sin pausar manualmente |

- Límite clave: el reverse search **no** detecta fakes creados desde cero (no hay copia previa); sirve sobre todo para material **reutilizado** (face-swap conserva cuerpo/fondo; desastre antiguo subido como "de última hora").
- Fuentes: https://imgkey.com/verification-tools · https://bellingcat.gitbook.io/toolkit/more/all-tools/invid · https://neuraldefend.com/insights/deepfake-foundations/reverse-image-search

### 2.3 Verificación de metadatos
- **ExifTool** (Phil Harvey): CLI de referencia para extraer/escribir metadatos EXIF/XMP/IPTC de casi cualquier formato (imagen, vídeo, audio). Gratis, open source, mantenido desde 2003. **Por qué:** revela modelo de cámara, GPS, timestamps, historial de edición; "qué lleva realmente el archivo".
- **Metadata2Go / Pic2Map**: visores web de EXIF (subir a tercero = riesgo OPSEC).
- **Amnesty YouTube DataViewer** (citizenevidence.amnestyusa.org): extrae el **timestamp exacto de subida** de un vídeo de YouTube y genera miniaturas para búsqueda inversa. Gratis. **Por qué:** verifica si el material apareció antes de la fecha declarada.
- Fuentes: https://imgkey.com/verification-tools · https://resources.rsf.org/work-with-open-source-intelligence-part-2-extracting-information-from-online-videos

### 2.4 Detección de deepfakes / manipulación
- **InVID-WeVerify / VeraAI (Deepfake Tab):** plugin Chrome/Firefox (v0.93, act. 2026-07); análisis forense de vídeo (keyframes, OCR, ELA, análisis de ruido, dominio de frecuencia), búsqueda en 6 motores y *Database of Known Fakes*. Gratis. **Cuidado:** la pestaña deepfake es experimental; tratar puntuaciones como **pistas**, no probabilidades calibradas.
- **Deepware Scanner** (web, gratis), **AI or Not** (consumo), **Hive** (API comercial), **Sensity** (plataforma enterprise), **Reality Defender** (comercial, informes para tribunales), **Intel FakeCatcher** (rPPG: microvariaciones de color de piel por flujo sanguíneo). Mixto gratis/pago.
- **Content Credentials / C2PA Verify** (contentcredentials.org/verify) y **c2patool**: verifican **procedencia firmada** (watermarking/firmas). Gratis. **Clave:** la ausencia de credencial **no** prueba que sea falso; una credencial válida no prueba que el evento ocurriera.
- **FotoForensics** (ELA): chequeo rápido; gratis/freemium. **Mal uso:** tomar el ELA como veredicto.
- **Amped Authenticate**: estándar forense comercial para uso en tribunales (validado, con procedimientos documentados). Pago.
- **Metodología de evaluación defensible (multi-señal, no un solo veredicto):** (1) metadatos (ExifTool), (2) artefactos visuales (iluminación cara/fondo, orejas/dientes, reflejos oculares), (3) reverse image search (procedencia), (4) ≥2 detectores (el desacuerdo es señal), (5) cadena de procedencia (quién lo publicó primero).
- Fuentes: https://deepfakecheck.io/blog/best-free-deepfake-detectors-2026 · https://www.mdpi.com/1858-... (review IIASA: https://pure.iiasa.ac.at/id/eprint/21428/1/information-17-00347.pdf) · https://intelligencenotes.com/08-Guides--and--Manuals/Tool-Guides--and-Workflows/OSINT-Toolkit-Essentials

### 2.5 Cronolocalización (cuándo) y geolocalización (dónde)
- **SunCalc** (suncalc.org): modela posición del sol (azimut/elevación) y longitud/dirección de sombras según fecha, hora y lugar. Gratis. **Por qué:** una sombra es "un reloj y un calendario"; permite estimar la hora (y acotar fecha/lugar) con trigonometría, sin conjeturas. Existe librería Python `suncalc`.
- **Bellingcat Shadow Finder Tool**: automatiza la búsqueda de todas las ubicaciones de la Tierra compatibles con una razón altura/objeto–sombra + fecha/hora. Gratis. **Por qué:** reduce el área de búsqueda global a unos pocos países.
- **Google Earth Pro / Timelapse**, **Sentinel Hub EO Browser** (ESA, gratis), **Planet Labs** (freemium), **USGS EarthExplorer**, **Maxar** (comercial): imágenes satelitales/históricas para confirmar layout y cambios en el tiempo.
- **Mapillary / KartaView / Bing Streetside / Google Street View**: verificación a nivel de calle (ground truth).
- **Geolocalización por señales visuales:** idioma en carteles, matrículas, arquitectura, vegetación, infraestructura eléctrica, marcas viales.
- **IA de geolocalización (2026):** **GeoSeer** (agéntico, multi-imagen/vídeo/texto; free tier + planes desde ~$19/mes; API), **GeoAxis**, **Oceanir**, **Picarta**, **GeoInfer** (transparencia-first), y **GeoSpy → renombrado Raven** (Graylark; acceso restringido a agencias verificadas desde Q1 2025). **Advertencia de rigor:** las cifras de acierto (p. ej. GeoSeer 67% @1km en IM2GPS3k) son **autodeclaradas** y no reproducidas independientemente *[a verificar]*. Usar como **generador de candidatos**, no como prueba.
- Fuentes: https://www.bellingcat.com/resources/2024/08/22/shadow-geolocate-geolocation-locate-image-tool-open-source-bellingcat-measure/ · https://www.bellingcat.com/resources/2021/05/18/unsure-when-a-video-or-photo-was-taken-how-to-tell-by-measuring-the-length-of-shadows · https://bellingcat.gitbook.io/toolkit/more/all-tools/suncalc · https://geoseeer.com/blog/best-ai-photo-location-finders-2026 · https://www.heise.de/en/news/Graylark-closes-public-access-to-AI-tool-for-geolocation-10252293.html

---

## 3. Herramientas y agentes de IA/LLM para OSINT

### 3.1 Servidores MCP (Model Context Protocol) de OSINT
MCP conecta herramientas/servicios con asistentes LLM (Claude, Cursor, Codex, Gemini CLI, OpenCode, etc.), permitiendo que un agente **encadene** herramientas y compile informes. Listas curadas:
- **awesome-osint-mcp-servers** (soxoj / OSINT-Experts-Society / WendigosCyber): catálogos de servidores MCP por categoría (SOCMINT, threat intel, geo, blockchain, research, media verification, scraping). Gratis/open source.
- **osint-toolbox-mcp** (renkagod, MIT, 2026-09): 12 herramientas clásicas locales **sin API keys** (Sherlock, Maigret, Blackbird, Holehe, GHunt, theHarvester, SpiderFoot, subfinder, dnstwist, dnsrecon, PhoneInfoga, ExifTool) + WHOIS/DNS/crt.sh/Wayback. Docker o `uvx`.
- **frishtik/osint-tools-mcp-server** (MIT, Python/asyncio): envuelve Sherlock, Holehe, SpiderFoot, GHunt, Maigret, theHarvester, Blackbird.
- **OSINT Tools MCP** (Python): envuelve 7 CLIs (Sherlock, Blackbird, Maigret, Holehe, GHunt, theHarvester, SpiderFoot).
- Otros MCP de interés: **Maigret MCP** (username), **Shodan MCP** (infra), **VirusTotal MCP** (threat intel), **Wayback Machine MCP** (npx mcp-wayback-machine), **IPInfo**, **Parallel/You.com** (web search), **Voidly** (censura/OONI), **Tanod/Vend** (blockchain, pay-per-call).
- **Por qué sirven:** convierten herramientas dispersas en flujos **autónomos y reproducibles**; el agente decide qué ejecutar y encadena hallazgos.
- Fuentes: https://github.com/soxoj/awesome-osint-mcp-servers · https://github.com/OSINT-Experts-Society/directory-soxoj-awesome-osint-mcp-servers · https://github.com/WendigosCyber/Awesome_OSINT_MCP_Servers · https://github.com/renkagod/osint-toolbox-mcp · https://github.com/frishtik/osint-tools-mcp-server · https://projectosint.substack.com/p/the-definitive-list-of-mcp-servers

### 3.2 Agentes autónomos de OSINT
- **OpenOSINT** (MIT, PyPI `openosint`, 21 herramientas; REPL + MCP + Claude Code plugin + Web UI; pasivo por defecto; soporta Anthropic Claude o **Ollama local**): cada hallazgo cita la llamada que lo produjo; grafo de entidades tipo FollowTheMoney con procedencia. Gratis/open source. https://github.com/OpenOSINT/OpenOSINT
- **SYNINT** (gs-ai, v5): framework **local-first** multi-agente (46 agentes), ejecución por etapas, registro de evidencia y entidades, `chain_of_custody.jsonl`, reporte forense. Gratis/open source. https://github.com/gs-ai/SYNINT
- **agentic-osint-agent** (thunderstornX): agente ReAct en LangGraph, 5 herramientas read-only, **ledger de evidencia determinista** (el LLM no etiqueta evidencia, solo decide y resume). Gratis. https://github.com/thunderstornX/agentic-osint-agent
- **ARES** (VENUENGG, 2026-10): plataforma "evidence-backed, policy-governed"; principio "el LLM no es la fuente de verdad"; motor de políticas que media cada llamada; almacenamiento de evidencia append-only. https://github.com/VENUENGG/ARES
- **osint-agent** (blaikr, Apache-2.0): LangGraph + Claude Haiku + SearXNG + Crawl4AI + ChromaDB; búsqueda multilingüe (16 idiomas), memoria persistente, imágenes satelitales. https://github.com/blaikr/osint-agent
- **OWASP SocialOSINTAgent** (OWASP, proyecto "other"): agente autónomo con LLM texto+visión vía API OpenAI-compatible; agrega actividad en X/Reddit/HN/Bluesky/GitHub/Mastodon y responde consultas en lenguaje natural. https://owasp.org/projects/socialosintagent
- **Spotlight** (Buried Signals): "research swarm" + investigador + **fact-checker independiente** + 26 skills; corre en local; el humano aprueba cada "gate". http://spotlight.buriedsignals.com/
- **Blue Helix** (Infoblox, 2026-11): agente OSINT de threat intel que orquesta MCP servers y rellena formularios de indicadores para revisión humana. https://www.infoblox.com/blog/security/blue-helix-agentic-osint-researcher
- **Por qué sirven / advertencia:** aceleran recolección y correlación, pero **no sustituyen el juicio analítico**; riesgo de alucinación si el LLM "etiqueta" evidencia. Los mejores diseños usan **colectores deterministas** y mantienen "human-in-the-loop".

### 3.3 LLMs locales para privacidad
- **Ollama** (MIT): corre modelos locales; inferencia local real, pero **sin auth por defecto** en el puerto 11434 (escaneo Censys/SentinelLABS ene 2026 halló ~175.108 hosts Ollama expuestos, >48% con tool-calling). Fijar `OLLAMA_HOST=127.0.0.1`. https://ollama.com/privacy
- **LM Studio**: sin telemetría de usuario por defecto (sí checks de actualización); soporta inferencia cloud opcional. 
- **llama.cpp**: C++ puro, sin stack de red ni telemetría; ideal **air-gapped**. 
- **GPT4All / Jan / Open WebUI**: alternativas locales (auditar telemetría).
- **Riesgos reales (probados con capturas de paquetes 2026):** API sin auth, binding a `0.0.0.0`, telemetría/fingerprints de clientes, reenvío de conversaciones tras errores, y **tools/plugins MCP que envían la consulta a terceros** (un modelo local con búsqueda web deja de ser local).
- **Por qué sirven:** permiten análisis OSINT **sin exfiltrar prompts/datos sensibles**; esenciales para casos con fuentes protegidas o datos personales (GDPR).
- Fuentes: https://localmodelbench.com/is-your-local-llm-actually-local · https://www.local-llm.net/blog/local-ai-privacy-audit/ · https://arxiv.org/html/2609.18526 · https://www.sans.org/blog/your-local-ai-server-is-not-local-finding-exposed-ollama-hosts-without-crossing-line · https://arxiv.org/html/2603.23996 (implicaciones forenses de LLMs locales)

---

## 4. Automatización con Python

Python es el lenguaje dominante del ecosistema OSINT (sintaxis rápida, librerías para HTTP/HTML/APIs/NLP/grafos/geo/imagen, y casi todos los frameworks públicos están en Python).

### 4.1 Frameworks y herramientas (Python)
| Herramienta | Función | Tipo | Por qué sirve |
|---|---|---|---|
| **SpiderFoot** (MIT) | +200 módulos de recolección, motor de correlación (37 reglas), Web UI + CLI + API REST, export CSV/JSON/GEXF, Tor | Gratis/open source (HX de pago) | "OSINT as a service" auto-hospedable; recon de superficie de ataque |
| **theHarvester** | Enumeración de correos/subdominios/hosts desde crt.sh, DNS, motores, repos | Gratis/open source | Primera parada en recon de dominio; CLI/REST/HarvestView |
| **Recon-ng** | Framework modular estilo Metasploit (marketplace de módulos) | Gratis/open source | Flujos reproducibles y scriptables |
| **Sherlock** | Username en 400+ sitios | Gratis | Estándar para barridos de usuario |
| **Maigret** (MIT) | Username en 10.000+ sitios, extrae perfil, recursivo, embebible como librería | Gratis | Dossier por username; `--ai` resume resultados |
| **Holehe** | Email registrado en ~120 plataformas (sin enviar resets) | Gratis | Enumeración por email |
| **GHunt** | Intel de cuenta Google por email/Gaia ID | Gratis | Perfil/pfp/reseñas Maps |
| **PhoneInfoga** | OSINT de número de teléfono | Gratis | Carrier/país/formatos |
| **Amass** | Descubrimiento de subdominios/activos a escala | Gratis | Mapeo DNS masivo |
| **Maltego** (CE gratis / CTAS de pago) | Mapeo de relaciones (persona–empresa–infra) | Freemium | Estándar de grafos; SDK TRX en Python |
| **OpenCTI** | Plataforma de gestión/ correlación de inteligencia | Gratis/open source | Almacenamiento a largo plazo |

- Fuentes: https://github.com/smicallef/spiderfoot · https://github.com/laramies/theHarvester · https://github.com/soxoj/maigret · https://intelligencenotes.com/08-Guides--and--Manuals/Tool-Guides--and-Workflows/Python-OSINT-Automation-Guide · https://dev.to/trulysoulless/self-hosted-osint-tools-in-2026-an-honest-spiderfootmaltego-alternatives-comparison-of4

### 4.2 Librerías Python por vector de recolección
- **HTTP/HTML:** `requests`, `httpx`, `BeautifulSoup4`, `Scrapy`, `Crawl4AI` (Playwright).
- **Metadatos:** `ExifRead`, wrappers de ExifTool, `pypdf`.
- **Red/DNS:** `ipwhois`, `dnspython`, `python-whois` (RDAP-aware).
- **Grafos/relaciones:** `networkx`.
- **Teléfonos:** `phonenumbers`.
- **Astronomía/geo:** `suncalc`.
- **Scraping social:** `snscrape`, `twint` (frecuentemente rotos por cambios de API *[a verificar]*).
- Fuentes: https://www.intel471.com/blog/python-libraries-for-osint-automation · https://github.com/tegridydev/python-OSINT-notebook

### 4.3 Buenas prácticas de automatización
- Ejecutar en **VM dedicada** (aislamiento OPSEC), con `uv`/venv; control de tasa y respeto de ToS; registrar cada llamada para la cadena de custodia. Scraping masivo: cuidado legal (hiQ v. LinkedIn: scraping de perfiles públicos no es violación de CFAA en EE.UU., pero sobreviven reclamaciones estatales/contractuales *[verificar jurisdicción]*).

---

## 5. Preservación de evidencia y cadena de custodia

### 5.1 Estándares y guías
- **SWGDE 18-F-002 v2.0 — Best Practices for Digital Evidence Collection** (actualizado 2025-11-20). Gratis. Puntos clave: crear copia estática local + documentar fuente; **hash criptográfico de adquisición** con **múltiples algoritmos** (evitar colisiones); hash de verificación tras adquirir; **documentación contemporánea** (software, logs, capturas, tamaños, nombres, hashes); **cadena de custodia** con identificador único, fecha/hora, y cada transferencia con nombre/firma; inventario de evidencia; sanitización de medios; seguridad física/lógica.
  Fuente: https://www.swgde.org/documents/published-complete-listing/18-f-002-2-0 · PDF: https://swgde.org/wp-content/uploads/2025/12/2025-11-20-Best-Practices-for-Digital-Evidence-Collection-18-F-002-2.0.pdf
- **NIST IR 8387 — Digital Evidence Preservation** (2022). Gratis. Enumera debilidades de la cadena de custodia: alterar antes de hashear; re-hashear y sobrescribir; colisiones MD-5/SHA-1; cambios accidentales. Recomienda almacenar hashes/firmas de forma que se pueda probar la no manipulación.
  Fuente: https://doi.org/10.6028/NIST.IR.8387
- **Berkeley Protocol** (preservación como fase del ciclo) y **Guía UNESCO para fiscales sobre evidencia digital** (preservación ≠ acceso; congelamiento de datos; minimización). Fuentes: https://unesdoc.unesco.org/ark:/48223/pf0000395060
- **Convenio de Budapest (Convenio sobre Cibercriminalidad), Arts. 16–17:** preservación expedita ("congelamiento") de datos informáticos almacenados; **Red 24/7** de puntos de contacto. Fuente: https://www.coe.int/en/web/cybercrime/the-budapest-convention
- **C2PA / Content Credentials** (especificación 2.4, dic 2025; soporte de streaming en vivo, OGG Vorbis): procedencia criptográfica firmada (hard/soft bindings). Gratis/abierto. **Clave:** la procedencia aporta señal afirmativa de origen, pero su ausencia no prueba manipulación.
  Fuente: https://spec.c2pa.org/specifications/specifications/2.4/specs/C2PA_Specification.html

### 5.2 Herramientas de captura/archivo y preservación
| Herramienta | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| **Hunchly** (adquirido por Maltego, may 2025) | Captura automática de cada página visitada (URL, timestamps, **hash criptográfico**, captura full-page); GPG-sign; genera paquetes "court-ready" con pista de auditoría | Pago (prueba 30 días) | Preserva **el rastro investigativo completo**, no solo la página; estándar para casos legales |
| **Wayback Machine / archive.org** + **archive.today / ghostarchive** | Snapshots de páginas; CDX API | Gratis | Evidencia de que el contenido existió en fecha X (aunque la fuente lo borre) |
| **c2patool** | Inspección scriptable/archival de manifests C2PA | Gratis/open source | Salida verbosa = salida correcta para archivo |
| **ExifTool** | Extrae/normaliza metadatos | Gratis | Documenta procedencia técnica del archivo |
| **Funciones hash del SO** (`shasum`, `certutil`, `sha256sum`) | Huella tamper-evident | Gratis | Verificación de integridad |
| **SYNINT** | `chain_of_custody.jsonl`, `investigation.sqlite`, artefactos crudos/renderizados por corrida | Gratis/open source | Registro de custodia automatizado a nivel de framework |

- **Buenas prácticas (Alliance4Europe / Berkeley):** registrar por cada acción: *timestamp*, *consulta/URL/herramienta*, *actividad*, *evidencia recogida*, *fuente*, *notas del investigador*. Archivar siempre (capturas + hash + firma) porque el contenido puede borrarse/editarse.
  Fuente: https://alliance4europe.eu/wp-content/uploads/2025/12/OSINT-Best-Practices-Repository-%E2%80%93-Alliance4Europe-%E2%80%93-November-2025.pdf

### 5.3 Formatos y estándares a documentar
- **Hash:** SHA-256 (mínimo) + segundo algoritmo (SHA-512/Whirlpool) para evitar colisiones.
- **Metadatos:** EXIF/XMP/IPTC (imagen), contenedores de vídeo/audio.
- **Procedencia:** Content Credentials (C2PA).
- **Cadena de custodia:** registro contemporáneo con identificador único, fecha/hora, transferencias firmadas, inventario.
- **Export:** CSV/JSON/GEXF (SpiderFoot), DOCX/PDF con hash y firma (Hunchly), JSON de reporte con procedencia (agentes).

---

## Resumen operativo (checklist para la VM)

1. **Planificar** con 5W+H y alcance/OPSEC; aislar en VM.
2. **Recolectar** con SpiderFoot/theHarvester/Maigret/Holehe (o vía MCP/agente) y **archivar** con Hunchly/Wayback + hash SHA-256 desde el primer byte.
3. **Procesar** (traducción, OCR, normalización) y **verificar** con triangulación + SIFT + reverse image (Yandex+TinEye+Google) + ExifTool + SunCalc/geolocalización + ≥2 detectores deepfake; tratar todo resultado automático como **probabilístico**.
4. **Analizar** con ACH (matriz evidencia×hipótesis, refutar) para minimizar sesgo y falsos positivos.
5. **Preservar y documentar** según SWGDE/NIST/Berkeley: hash múltiple, cadena de custodia contemporánea, inventario, C2PA cuando exista.
6. **Distribuir** con trazabilidad total (cada afirmación → fuente/llamada) y **retroalimentación**.
7. Si se usan **LLMs locales**, fijar binding a loopback, sin auth expuesta, y recordar que plugins MCP/web rompen el perímetro local.

---

### Advertencias de rigor (no confirmado / a verificar)
- Cifras de precisión de herramientas de geolocalización IA (GeoSeer/GeoInfer/Picarta/Oceanir) son **autodeclaradas**, no reproducidas por terceros.
- Disponibilidad/estado de herramientas ACH clásicas (PARC ACH 2.0, DECIDE, Decision Command) no verificada en 2026.
- Precios y funciones de Hunchly, GeoSeer, Raven, Reality Defender, Sensity, Amped cambian con frecuencia; confirmar en la fuente.
- Estado de scrapers sociales (twint/snscrape) puede estar roto por cambios de API de las plataformas.
- URL corporativa del Cyber Kill Chain (Lockheed Martin) no verificada en esta sesión; el marco es de dominio público.