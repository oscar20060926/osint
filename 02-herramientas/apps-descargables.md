# Informe OSINT 2026 — Mejores Aplicaciones Descargables (GUI de escritorio y móviles)

> Investigación basada en fuentes públicas consultadas en noviembre de 2026. Precios y disponibilidad verificados en las páginas oficiales/proveedores citados; pueden cambiar.

---

## 1. Resumen: las 15 mejores aplicaciones descargables OSINT

Ordenadas por utilidad/popularidad combinada en flujos de investigación reales (no por precio).

| # | Aplicación | Categoría | Plataforma | Modelo | Por qué destaca |
|---|------------|-----------|------------|--------|-----------------|
| 1 | **Maltego Graph (Desktop)** | Link analysis / grafos | Win · macOS · Linux | Freemium (Basic gratis; Pro €7.500/año) | Estándar de la industria para análisis visual de relaciones; 120+ partners de datos, transforms, informes. Base de Kali/Parrot. |
| 2 | **Google Earth Pro** | Geolocalización / GeoINT | Win · macOS · Linux | Gratuita | Globo 3D, imagen histórica (time slider), medición, KML/KMZ. La 2ª herramienta favorita de investigadores OSINT (encuesta Bellingcat 2022). |
| 3 | **SpiderFoot** | Recon automatizado | Win · macOS · Linux (UI web local) | Gratuita / open source (MIT) | 200+ módulos, motor de correlación, export CSV/JSON/GEXF. Cobertura masiva "apunta y dispara". |
| 4 | **Hunchly** | Captura/preservación de evidencia | Win · macOS · Linux + extensión Chrome | Freemium (Basic gratis; Classic 169 USD/149 € año) | Captura automática con hash SHA-256, cadena de custodia, informes DOCX/PDF aptos para tribunales. Adquirida por Maltego (2025). |
| 5 | **Autopsy** | Forense de disco / adquisición | Win · macOS · Linux | Gratuita / open source (Apache 2.0) | Plataforma forense E2E más usada; The Sleuth Kit, timeline, carving, EXIF, módulos. Estándar forense gratuito. |
| 6 | **Gephi** | Visualización de redes | Win · macOS · Linux | Gratuita / open source | Análisis y visualización de grafos de 10 a 10M nodos; ForceAtlas2, centralidad, detección de comunidades. |
| 7 | **ExifTool + GUI (v6) / Metadata++ / GeoSetter** | Metadatos / imágenes | Win (GUI) · macOS · Linux (CLI) | Gratuita / freemium | Lee/escribe EXIF, GPS, IPTC, XMP; geolocalización inversa integrada. La GUI v6 y Metadata++ lo hacen accesible sin terminal. |
| 8 | **FTK Imager** | Adquisición forense | Windows | Freemium (gratis; Pro de pago) | Estándar de facto para imágenes forenses E01/raw con verificación hash; preview/triage. |
| 9 | **Cytoscape Desktop** | Visualización de redes | Win · macOS · Linux | Gratuita / open source | Redes complejas, +100 apps/plugins, formatos estándar, análisis de centralidad y clustering. |
| 10 | **IBM i2 Analyst's Notebook** | Link analysis forense | Windows | De pago (enterprise) | Estándar en fuerzas del orden y grandes empresas; análisis "courtroom-friendly" de conexiones, flujos y eventos. |
| 11 | **NodeXL** | Análisis de redes sociales | Windows (plugin Excel) | Freemium (Basic gratis; Pro de pago) | Importa redes de X/Bluesky/Reddit/YouTube; métricas y visualización dentro de Excel. Curva de entrada baja. |
| 12 | **Ferret OSINT** | Toolkit OSINT móvil | Android · iOS | Gratuita | DNS, WHOIS, subdominios, email harvesting; todo local, cifrado AES-256, sin cuentas. Privacidad-first. |
| 13 | **Maigret (app/scripts)** | Username / perfiles | Android · iOS · escritorio | Gratuita / open source | 3.000+ sitios, perfil ampliado; interfaz web/app. Fork avanzado de Sherlock. |
| 14 | **SIFT Workstation** | Forense / IR (VM Linux) | Linux (VM) | Gratuita (SANS) | Appliance Linux bootable con herramientas forenses curadas, hashing y triage repetible. |
| 15 | **Raven (antes GeoSpy)** | Geolocalización por imagen (IA) | Web/app (enterprise) | De pago (gobierno/empresa) | Localiza imágenes sin metadatos por visión artificial; street-level, identificación de vehículos, detección de manipulación. |

---

## 2. Tablas por categoría

### 2.1 Suites OSINT con GUI / Link analysis
| Herramienta | Instalación | Qué hace | Modelo | Destaca por |
|-------------|-------------|----------|--------|-------------|
| Maltego Graph Desktop | Win/macOS/Linux (Java) | Grafo de entidades + transforms | Freemium (Basic €0/200 créditos; Entry €3.000; Pro €7.500/año) | Referencia visual; 120+ partners; Maltego One (browser) desde oct-2025 |
| SpiderFoot | Win/macOS/Linux (Python, UI web local :5001) | 200+ módulos, correlación, Tor | Gratis (MIT); HX integrado en Intel 471 | Automatización masiva; export GEXF a Gephi |
| IBM i2 Analyst's Notebook | Windows | Charting de conexiones/flujos/eventos | De pago | Estándar forense en ley y empresa |
| Lampyre | Windows | Pivots estilo Maltego + triage | De pago (más barato) | Alternativa económica a Maltego |

### 2.2 Análisis de imágenes y metadatos
| Herramienta | Instalación | Qué hace | Modelo | Destaca por |
|-------------|-------------|----------|--------|-------------|
| ExifTool | Win/macOS/Linux (Perl/CLI) | Lee/escribe EXIF, GPS, IPTC, XMP, GeoTIFF | Gratis (open source) | Soporta más etiquetas que ningún otro; geolocalización inversa |
| ExifToolGUI v6 | Windows | GUI para ExifTool | Gratuita | Interfaz gráfica mantenida del motor ExifTool |
| Metadata++ | Windows | Ver/editar/extraer metadatos | Freemium | GUI pulida, batch |
| GeoSetter | Windows | Geotagging por mapa | Gratuita | Cambio de datos GPS de imágenes |
| Raven (ex-GeoSpy) | Web/app enterprise | Geolocalización por IA sin metadatos | De pago | Precisión a nivel de calle; detección de manipulación |

### 2.3 Geolocalización / GeoINT
| Herramienta | Instalación | Qué hace | Modelo | Destaca por |
|-------------|-------------|----------|--------|-------------|
| Google Earth Pro | Win/macOS/Linux | Globo 3D, imagen histórica, medición | Gratuita | Time slider histórico; descargas nuevas finalizan 25-jun-2027 |
| Google Earth (móvil/web) | Android/iOS/Web | Exploración geográfica | Gratuita | Geolocalización sobre la marcha |
| Mapillary / KartaView | Web/app | Street-level crowdsourced | Freemium | Cobertura donde Street View no llega |
| Sentinel Hub Playground | Web | Visualización satelital Sentinel | Freemium | Archivo Sentinel ~10 m gratis |

### 2.4 Forense / adquisición de datos
| Herramienta | Instalación | Qué hace | Modelo | Destaca por |
|-------------|-------------|----------|--------|-------------|
| Autopsy | Win/macOS/Linux (Java) | Análisis de imágenes de disco | Gratis (Apache 2.0) | E2E forense; timeline, carving, EXIF, módulos |
| FTK Imager | Windows | Imágenes forenses E01/raw + hash | Freemium (Pro de pago desde oct-2025) | Estándar de adquisición; preview/triage |
| SIFT Workstation | Linux (VM) | Suite forense/IR preconfigurada | Gratuita (SANS) | Triage repetible y reproducible |
| Eric Zimmerman Tools | Windows | Parsing de artefactos (registry, shellbags) | Gratuitas | Análisis de artefactos Windows |
| Volatility 3 | Win/Linux (CLI) | Análisis de memoria RAM | Gratis (open source) | Forense de memoria de referencia |
| Wireshark | Win/macOS/Linux | Captura/análisis de red | Gratis (open source) | Forense de tráfico de red |

### 2.5 Visualización de redes / grafos
| Herramienta | Instalación | Qué hace | Modelo | Destaca por |
|-------------|-------------|----------|--------|-------------|
| Gephi | Win/macOS/Linux | Layouts + métricas de grafos | Gratis (open source) | ForceAtlas2, centralidad, comunidades |
| Cytoscape Desktop | Win/macOS/Linux (Java) | Redes complejas + apps | Gratis (open source) | +100 plugins; formatos estándar |
| NodeXL | Windows (plugin Excel) | Redes sociales en Excel | Freemium | Importadores X/Bluesky/Reddit/YouTube |
| Neo4j + Bloom | Win/Mac/Linux/Docker | Base de datos de grafos + viz | Freemium/comercial | Consulta Cypher; escala muy grande |
| yEd | Win/macOS/Linux | Diagramas manuales | Gratuita | Diagramas limpios y controlados |

### 2.6 Monitorización / scraping con interfaz
| Herramienta | Instalación | Qué hace | Modelo | Destaca por |
|-------------|-------------|----------|--------|-------------|
| SpiderFoot HX / Intel 471 | Cloud (gestionado) | Monitorización de superficie de ataque | De pago | Alertas de cambio, multiusuario, API REST |
| Hunchly (Cloud) | Navegador (Kasm Workspaces) | Captura de evidencia en la nube | De pago (contactar ventas) | Investigación desde cualquier equipo |
| Social Links (SL Professional) | Windows (enterprise) | OSINT de redes 500+ plataformas | De pago (enterprise) | Reconocimiento facial, geolocalización, integra Maltego |
| Hootsuite / Meltwater | Web/app | Escucha de redes y sentimiento | Freemium/de pago | Monitorización de marca y desinformación |

### 2.7 Apps móviles OSINT (Android / iOS)
| App | SO | Qué hace | Modelo | Destaca por |
|-----|----|----------|--------|-------------|
| Ferret OSINT | Android · iOS | DNS, WHOIS, subdominios, email harvest | Gratuita | Todo local, AES-256, sin cuentas |
| Maigret | Android · iOS | Username → perfiles (3.000+ sitios) | Gratuita/open source | Perfil ampliado; muy popular (4,5★) |
| Sherlock-OSINT | iOS | Username search | Gratuita (con anuncios/IAP) | Simple y rápido |
| OSINT Researcher | iOS | Explora orgs/repos de GitHub | Freemium | Útil para devs y reclutadores |
| TraceSeek | iOS | Búsqueda de identidad digital | Freemium | Interfaz móvil pulida |
| World Monitor | iOS | Mapa de eventos en vivo | Gratuita | OSINT geopolítico en tiempo real |
| Google Earth | Android · iOS | Globo 3D móvil | Gratuita | Geolocalización de campo |

---

## 3. Tablas por sistema operativo

### Windows
- Maltego Graph Desktop · SpiderFoot · Hunchly · Autopsy · FTK Imager · ExifToolGUI v6 · Metadata++ · GeoSetter · Gephi · Cytoscape · NodeXL · IBM i2 Analyst's Notebook · Eric Zimmerman Tools · X-Ways Forensics · Ferret OSINT (vía emulador no; app nativa móvil)
### macOS
- Maltego Graph · SpiderFoot · Hunchly · Google Earth Pro · Autopsy · ExifTool (CLI) · Gephi · Cytoscape · Wireshark
### Linux
- Maltego Graph · SpiderFoot · Hunchly (Ubuntu 20.04+) · Google Earth Pro · Autopsy · ExifTool · Gephi · Cytoscape · SIFT Workstation · Volatility 3 · Wireshark
### Android
- Ferret OSINT · Maigret · Google Earth · Maltego (vía web/servicios) · apps de monitoreo
### iOS
- Ferret OSINT · Maigret · Sherlock-OSINT · OSINT Researcher · TraceSeek · World Monitor · Google Earth

> Nota: la mayoría de suites "pesas pesadas" (Maltego, SpiderFoot, Autopsy, Gephi) son multiplataforma de escritorio. En móvil, el ecosistema OSINT es más ligero y se apoya en apps de lookups y en navegación web.

---

## 4. Notas de uso responsable y legal

- **Legalidad base:** recopilar información pública es, en general, legal. Se vuelve ilegal al acceder a cuentas/sistemas privados, eludir logins, acosar o espiar, o tratar datos personales incumpliendo el RGPD/UK GDPR y leyes locales.
- **Autorización y propósito legítimo:** usa estas herramientas solo con base legal y propósito legítimo (investigación profesional autorizada, due diligence, periodismo, seguridad propia). Documenta fuentes y cadena de custodia.
- **OPSEC del investigador:** algunas consultas revelan tu interés en el objetivo. Para investigaciones sensibles, opera desde infraestructura no atribuible (VPN/VM dedicada) y considera el "passive" mode de SpiderFoot.
- **Evidencia y tribunales:** captura con hash (Hunchly), preserva metadatos (ExifTool) y sigue protocolos reconocidos (NIST SP 800-86, Berkeley Protocol, reglas locales de admisibilidad).
- **Privacidad:** minimiza datos, no subas imágenes de terceros a servicios desconocidos (usa herramientas locales como ExifTool/ShadowDragon Image Forensics), y respeta los términos de las plataformas.
- **Herramientas de monitorización/spyware:** evita software de vigilancia encubierta (mSpy, FlexiSPY, etc.); su uso sin consentimiento es ilegal en la mayoría de jurisdicciones.
- **Doble uso:** el OSINT es legal; el hacking no. La frontera es el acceso no autorizado.

---

## 5. Fuentes principales

- Maltego — maltego.com (pricing, Graph Desktop, adquisición de Hunchly may-2025)
- SpiderFoot — github.com/smicallef/spiderfoot ; spiderfoot.net (HX → Intel 471)
- Hunchly — hunch.ly (pricing, planes, requisitos) ; Bellingcat Toolkit
- Autopsy — autopsy.com ; Sleuth Kit Labs ; comparativas Cyber Triage 2026
- ExifTool — exiftool.org (v13.64, geolocation, GUIs)
- Google Earth Pro — bellingcat.gitbook.io/toolkit ; google.com/earth/about/versions (fin descargas 25-jun-2027)
- Gephi — gephi.org ; Cytoscape — cytoscape.org ; NodeXL — smrfoundation.org/nodexl
- Raven (ex-GeoSpy) — graylark.com/raven ; geospy.ai
- Ferret OSINT — Google Play / App Store ; appshunter.io (ranking iOS 2026)
- ShadowDragon, OSINTsearch, Clearfront, Ransomnews, Espectrosint, OSINTPanel (comparativas 2026)
- EEAS OSINT Guidelines 2024 (PDF) ; Cyber Triage Forensic Tools Comparison 2026