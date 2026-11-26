# OSINT Especializado por Vertical — Informe 2026

> Investigación OSINT por verticales: herramientas, técnicas y fuentes. Elaborado con búsqueda web (2026). Donde un dato no se pudo confirmar se indica explícitamente. Muchas herramientas cambian de precio/estado con rapidez: verificar antes de operar.

## Índice
1. Geolocalización y cronolocalización (GEOINT)
2. Verificación de imágenes y vídeo (incl. deepfakes)
3. OSINT financiero y corporativo
4. OSINT de telefonía
5. OSINT de email y filtraciones
6. Seguimiento aéreo y marítimo
7. OSINT de redes sociales por plataforma
8. OSINT de documentos y metadatos avanzados
9. OSINT de infraestructura y threat intelligence (CTI)

---

## 1. Geolocalización y cronolocalización (GEOINT)

**Qué es:** determinar *dónde* (geolocalización) y *cuándo* (cronolocalización) se capturó una imagen/vídeo a partir de pistas visibles, metadatos, sombras, meteorología y datos de transporte.

### Técnicas clave
- **Coincidencia visual de landmarks:** arquitectura, señalización, mobiliario urbano (farolas, semáforos, bollardos), marcas viales, tendido eléctrico, vegetación, terreno.
- **Consultas OSM combinadas** (Overpass Turbo / Bellingcat OSM Search): cruzar 2–3 objetos distintivos para reducir un país a un puñado de candidatos.
- **Análisis de sombras (cronolocalización física):** longitud = altura / tan(elevación solar); azimut marca la dirección. Con latitud + fecha acota hora (±~30 min) y rango de fechas.
- **Meteorología e incendios:** comparar con archivos históricos (Weather Underground, NOAA, EUMETSAT, NASA FIRMS, Ventusky, Nullschool).
- **Vegetación estacional, matrículas, modelos de móvil, carteles** como marcadores temporales.
- **Regla de oro:** exigir 3+ coincidencias independientes; la IA genera candidatos, no pruebas.

### Herramientas
| Herramienta | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| Google Earth Pro | Imagen satelital histórica, 3D, medición, *sunlight tracker* | Gratis | Base de trabajo; superponer captura sobre modelo 3D |
| Google Maps / Street View | Verificación a nivel de calle con *time slider* | Gratis | Confirmar edificios/murales/obras en fecha |
| Yandex Maps / Bing / Apple / Baidu / Gaode | Cobertura regional (Europa del Este, Asia) | Gratis | Rellenan huecos donde Google falla |
| Mapillary / KartaView | Street-level colaborativo | Gratis (freemium) | Zonas rurales/industriales sin Street View |
| OpenStreetMap + Overpass Turbo / Bellingcat OSM Search | Consultas geográficas combinadas | Gratis | Reduce área de búsqueda por objetos |
| SunCalc.org | Posición solar y dirección de sombra por fecha/lugar | Gratis | Cronolocalización por sombras |
| Bellingcat Shadow Finder | Inverso: dada sombra+altura+fecha, devuelve banda de latitudes | Gratis (MIT, Colab) | Restringe "cualquier lugar" a una franja |
| PhotoPills | App de fotografía con RA solar | Pago | Escenas y horas exactas |
| ShadeMap / ShadowCalc | Sombras de terreno/edificios 3D | Freemium | Oclusión por relieve (valles) |
| Stellarium | Planetario open-source | Gratis | Noche/crepúsculo, estrellas |
| ExifTool / GeoSetter | Metadatos GPS/EXIF | Gratis | Coordenadas y timestamps (si sobreviven) |
| Copernicus Browser, Sentinel Hub EO Browser, NASA Worldview, Planet, Maxar, EarthExplorer | Satélite óptico/SAR | Freemium/pago | Confirmar explosiones, inundaciones, convoyes |
| QGIS | SIG de escritorio | Gratis | Proyectos reproducibles, superposición |
| GeoHints | Catálogo de "tells" regionales | Gratis | Entrenar el ojo |
| Picarta, GeoSpy/Raven, GeoSeer, GeoInfer, GeoAxis | IA de geolocalización por píxeles | Freemium/pago | Generar hipótesis cuando EXIF fue borrado |
| PeakVisor | Identificación de montañas | Freemium | Skyline como pista |
| Google Lens, Yandex Images, TinEye, Bing Visual Search | Búsqueda inversa | Gratis | Hallar la publicación original (a menudo resuelve antes de geolocalizar) |

**Retos:** Street View incompleto y desactualizado; revisita satelital con huecos; EXIF borrado por plataformas y falsificable; adversariales recortan/espejan; IA alucina con confianza; sesgo de confirmación (usar ACH); imprecisión de 1 px en sombra = cientos de km en Shadow Finder. *Fuentes:* bellingcat.com, cartelwatch.net, osintbay.com, intelligencenotes.com.

---

## 2. Verificación de imágenes y vídeo (incl. deepfakes)

**Enfoque (embudo, de menos a más esfuerzo):** 1) ¿es nueva? búsqueda inversa → 2) leer metadatos → 3) inconsistencias de escena → 4) contrastar con fuentes independientes → 5) análisis forense/procedencia. Ningún detector es concluyente por sí solo; convergencia de evidencia.

### Autenticación vs. verificación
- **Autenticación (procedencia):** C2PA / Content Credentials (firmas criptográficas de captura→edición).
- **Verificación (veracidad del contenido):** que la imagen muestre lo que dice mostrar.

### Herramientas
| Herramienta | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| InVID / WeVerify (v0.89, mar-2026) | Verificación de vídeo: búsqueda inversa, keyframes, logos, pestaña Deepfake (ensemble Xception/EfficientNet-B4/Capsule++) + Hiya (voz) + archivo WACZ | Gratis | Toolkit estándar de periodistas/fact-checkers (>57k usuarios/semana, según fuente) |
| FotoForensics | Análisis de nivel de error (ELA) | Freemium | Detectar zonas manipuladas |
| Forensically | ELA, clones, metadatos, C2PA | Freemium | Suite forense en navegador |
| ExifTool / Metadata2Go / Jimpl / xIFr / EXIF Purge | Metadatos EXIF/XMP | Gratis | Verificar dispositivo, fecha, GPS; detectar software de edición |
| C2PA Viewer / Content Credentials Verify | Inspeccionar procedencia firmada | Gratis | Cadena de custodia verificable |
| Google SynthID | Marca de agua de contenido IA de Google | Gratis | Confirmar origen IA (solo material Google) |
| Google Lens, Yandex, TinEye, PimEyes, RevEye, Search by Image | Búsqueda inversa / facial | Freemium | Encontrar usos previos, rostro |
| Search4Faces, FaceCheck.ID, ToolPie Face Comparison | Reconocimiento facial | Freemium/pago | Identificación (usar con cautela legal/ética) |
| AI or Not | % de probabilidad "IA/deepfake" | Freemium ($5/$100) | Señal rápida (usada por NYT según fuente) |
| Hive (ahora "Deploy") | Detección IA imagen/vídeo/audio + modelo generador | Pago (API) | Moderación a escala; 96–99,9% según proveedor |
| Sensity AI | Forense imagen/vídeo/audio | Pago (enterprise) | Investigación forense (~98% según proveedor) |
| Reality Defender | Enterprise, llamadas/reuniones; 50 escaneos gratis/mes | Freemium/pago | Detección en tiempo casi real |
| Deepware Scanner | Detector deepfake | Gratis (sin registro) | Prueba rápida |
| Intel FakeCatcher | Señal biológica (flujo sanguíneo) | Pago | Método físico, no aprendido |
| TrueMedia | Detección IA (imagen/audio) | Freemium | Uso periodístico |
| Pindrop, iProov | Antifraude de voz / liveness | Pago | Contact center / verificación de identidad |

**Audio:** Hiya (InVID), Deepfake Total, Deepfake-O-Meter; transcripción con oTranscribe, Google Pinpoint, Trint.
**Vídeo:** Azure AI Video Indexer, Amazon Rekognition; sincronía audio-labios (cross-correlación fonemas/apertura oral).

**Retos:** los detectores caen mucho fuera de distribución (compresión, nuevos generadores, post-proceso); benchmarks optimistas (FaceForensics++ 99% → 80% con compresión baja); ausencia de marca de agua **no** prueba autenticidad; una puntuación sin contexto engaña. *Fuentes:* citp.princeton.edu (guide ago-2026), aofirs.org (CIRS 2026), mdpi.com, acm.org, signalandshadow.io.

---

## 3. OSINT financiero y corporativo

**Objetivo:** identificar entidades, beneficiarios finales (UBO), sanciones, estructura societaria y riesgo.

### Fuentes y herramientas
| Recurso | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| SEC EDGAR | Filings de EE.UU. (10-K, 10-Q, 8-K, 13F, insider) + búsqueda full-text | Gratis | Base de compañías cotizadas EE.UU.; CIK, LEI, SIC |
| OpenCorporates | +245 M empresas en 145+ jurisdicciones; búsqueda avanzada y UBO | Web gratis; API pago (Essentials £2.250/año, Starter £6.600, Basic £12.000; acceso a escala gratis para beneficio público) | Registro mercantil global unificado |
| UK Companies House | Registro oficial UK, PSC (People with Significant Control), directores descalificados | Gratis | UBO y control en UK; datos oficiales |
| GLEIF (LEI) | Identificadores de entidad legal globales | Gratis | Desambiguar entidades por LEI |
| OpenSanctions | Agregador de listas de sanciones (OFAC, UE, ONU, UK, etc.) + enriquecimiento | Gratis no comercial; API pago | Cribado de sanciones y conexiones |
| OFAC SDN / Consolidated (US Treasury) | Listas de sanciones EE.UU. | Gratis | Fuente primaria; descarga directa |
| UK Sanctions List (FCDO/OFSI) | Sanciones UK | Gratis | Fuente primaria UK |
| EU Consolidated / UN Consolidated | Sanciones UE/ONU | Gratis | Cobertura multilateral |
| ICIJ Offshore Leaks Database | Panama/Pandora/Paradise Papers | Gratis | Estructuras offshore, sociedades pantalla |
| Open Ownership | Datos de beneficiarios finales | Gratis | Agregación/formats estandarizados |
| Aleph (OCCRP) | Base de datos de registros, filtraciones y empresas | Freemium | Búsqueda cruzada de entidades/personas |
| OpenCorporates + OpenSanctions (enriquecimiento) | Cruce registro↔sanciones | — | Conectar empresa sancionada con datos societarios |

**Técnicas:** resolver UBO por niveles de propiedad; distinguir nombre vs. control; usar LEI/registro para quitar homónimos; cruzar dirección compartida (p. ej. Offshore Leaks ↔ OpenSanctions) para hallar redes; adverse media; PEP. **Retos:** opacidad offshore, datos desactualizados, homónimos, portabilidad de jurisdicciones, cambios regulatorios (UE/UK/US divergentes). *Nota:* OpenCorporates **no** hace cribado de sanciones (confirmado por prometiam.com); para eso usar OpenSanctions/OFAC.

---

## 4. OSINT de telefonía

**Secuencia recomendada:** normalizar a E.164 → carrier + tipo de línea → sondeo de registro en plataformas → agregadores de personas (corroborar) → corpus de brechas.

| Herramienta | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| libphonenumber (Google) | Valida estructura y normaliza a E.164 | Gratis | Base de todo el flujo |
| PhoneInfoga | Formato, país, carrier, tipo; dorks de buscador (~17k★, último release v2.11.0 feb-2024) | Gratis/open source (necesita clave apilayer para carrier) | Estándar CLI/web; tratar DB de carrier como punto de partida |
| HLR Lookups (hlrlookup.com) | Consulta SS7/Diámetro: estado en vivo, operador actual, portabilidad, fecha de portado | Freemium (200 créditos gratis) | Resuelve carrier real (no prefijo) |
| 1Lookup | Estado en vivo + país + portado/roaming + carrier + MCC/MNC; CSV/API; MCP | Pago (5 créditos/consulta) | HLR + validación fijo/VoIP en mismos créditos |
| Twilio Lookup | Line Type Intelligence (mundial), SIM Swap (beta), Reassigned (US) | Pago (fracción de céntimo) | Corroboración carrier-grade |
| Infobip / Neutrino API / CheckMobi / Messente / seven.io | HLR/MNP/validación | Pago | Alternativas enterprise/desarrollador |
| Epieos | Reverse lookup email/teléfono; módulo Phone en nivel pago | Freemium/pago | Enlaza número↔identidad sin alertar |
| Phunter / SearchPhone / PhoneNumber-OSINT | Recopiladores multipropósito; SearchPhone añade inteligencia de infostealers (Hudson Rock) | Gratis/open source | Segunda opinión; filtraciones por número |
| Bellingcat Telegram Phone Number Checker | Comprueba si el número tiene Telegram y nombre visible | Gratis | Primer nombre real frecuente |
| WhatsApp OSINT (vía RapidAPI) | Foto de perfil, verificación, privacidad | Pago (API) | Señal de identidad (según privacidad) |
| DeHashed / LeakCheck / LeakRadar / IntelBase | Búsqueda por número en brechas | Freemium | Convierte número→email (a menudo el objetivo real) |
| That'sThem, USPhoneBook, Zabasearch, PeekYou, Spy Dialer, Whitepages; BeenVerified, Intelius | Agregadores de personas | Freemium/pago | Solo corroborar; datos rancios y solo EE.UU. |

**Retos y legal:** portabilidad (el prefijo no es el operador actual); HLR solo móvil (fijo/VoIP sin entrada); datos de personas son inferencias; **pretexting** de operador es delito federal en EE.UU. (Telephone Records and Privacy Protection Act 2006); GDPR exige base legítima. *Fuentes:* signalandshadow.io, 1lookup.io, osintcompass.com, osintguide.com, hlrlookup.com, checkmobi.com.

---

## 5. OSINT de email y filtraciones (más allá de HIBP)

| Herramienta | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| Have I Been Pwned (HIBP) | Brechas por email; API | Freemium | Referencia, pero solo por email |
| DeHashed | Motor de activos: credenciales, brechas, por email/usuario/teléfono/IP | Freemium | Búsqueda profunda; pivote por múltiples identificadores |
| LeakCheck | +10.000 M registros, 1366+ brechas; email/usuario/teléfono | Gratis/freemium | Cobertura amplia; gratis |
| IntelBase / LeakRadar | Índices de brechas | Freemium | Alternativas; búsqueda por número |
| Holehe | Comprueba en qué sitios (+120) está registrado un email, **sin alertar** | Gratis/open source | No envía correos de reset; silencioso |
| GHunt | Info de cuenta Google desde email/ID | Gratis/open source | Perfil Google (nombre, foto, YouTube, Maps) |
| Epieos | Reverse email → cuentas/enlaces | Freemium/pago | Enriquecimiento por email |
| Hunter.io | Verifica emails y busca por dominio | Freemium | Encontrar emails corporativos (patrón) |
| EmailRep | Reputación de email | Gratis | Señal de riesgo/validez |
| Infoga | OSINT de email | Gratis/open source | Recopilación |
| Sherlock / Maigret / WhatsMyName | Username → 400+ sitios | Gratis/open source | Pivote email↔usuario↔perfiles |
| Social Analyzer | Username/email en 600+ plataformas + perfilado IA | Freemium | Correlación masiva |
| SERPAPI / Google dorks | Búsqueda de patrones | Freemium | Encontrar exposición pública |

**Técnicas:** pivote email→username→redes; correlación de brechas; verificación de existencia sin alertar (Holehe); reputación. **Retos/legal:** muchas brechas son sensibles; GDPR; no todos los corpus indexan por número; verificar antes de reportar. *Fuentes:* dehashed.com, leakcheck.io, github.com/megadose/holehe, epieos.com, intelmind.io.

---

## 6. Seguimiento aéreo y marítimo

### Aéreo (ADS-B)
| Herramienta | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| Flightradar24 | Tracking en vivo por ADS-B + MLAT/fusión; historial | Freemium | Estándar civil; MH17 como caso canónico |
| ADS-B Exchange | ADS-B sin filtrar (militar/privado/bloqueados) | Freemium/pago | Lo que otros ocultan; patrones militares |
| FlightAware | Tracking + historial, AeroAPI | Freemium/pago | Cobertura y API |
| OpenSky Network | Red de receptores ADS-B, datos abiertos | Gratis (académico) | Dataset abierto para investigación |
| ADS-B (tecnología) | Transpondedor emite posición/identificación | — | Base física; *receiver* comunitarios |

### Marítimo (AIS)
| Herramienta | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| MarineTraffic | Mapa AIS en vivo, base de buques | Freemium | Estándar; posiciones e historial |
| VesselFinder | AIS en vivo, sin registro | Freemium | Alternativa; rutas/dockings |
| Equasis (EMSA) | Particularidades, propietario, clase, P&I, inspecciones; desde 2026 registro de transferencias ship-to-ship | Gratis (cuenta) | Primera parada de identidad del buque |
| Global Fishing Watch | Pesca/actividad oceánica por AIS desde 2012; Vessel Viewer | Gratis | Flotas fantasma, dark ships, patrones |
| MyShipTracking | Posiciones AIS en tiempo real | Freemium | Contrastar rutas |
| GISIS (IMO) | Datos de seguridad marítima | Gratis (cuenta) | Identidad/registro oficial |
| AIS (tecnología) | Identificación automática; satelital y terrestre | — | Base; gaps = "dark ships" |

**Técnicas:** correlacionar ADS-B/AIS con imágenes satelitales (Sentinel/Planet); detectar *dark ships* (AIS apagado), *spoofing*, transferencias ship-to-ship; rastrear propiedad corporativa del buque; patrones de flota. **Retos:** cobertura incompleta (militar/bloqueado), spoofing de AIS, gaps de satélite, y **privacidad**: buscar un buque logueado vincula tu interés a tu cuenta. *Fuentes:* flightradar24.com, osintnewsletter.com, adriadefense.com, socradar.io, github.com/atlas-bear/osint-tools, counterterrorismgroup.com.

---

## 7. OSINT de redes sociales por plataforma

> Nota general: el cierre de APIs (Reddit 2023, X) y las restricciones de scraping han degradado muchas herramientas; verificar fecha del último commit.

### X (Twitter)
- **BirdHunt, Sotwe, Nitter (mirrors, a menudo inestables), TweeterID** (fecha de creación), **Twitee, Twitter Trending Archive, twtData**, **TwOSINT** (perfil + hasta 3200 tweets, sin API oficial), **Twitter Intelligence (Kitploit)**. Búsqueda avanzada manual (rangos de fecha, filtros). *Tipo:* gratis/open source, fragilidad alta.

### Instagram
- **Instaloader** (descarga/archivo CLI), **Osintgram** (shell de análisis), **Osintly** (lookup por usuario), **Social Analyzer**. *Tipo:* gratis/open source; limitado por rate-limits.

### TikTok
- **TokIntel** (fecha de creación, datos ocultos), **Osintly TikTok lookup**, **OSINT Combine** (usernames/hashtags). *Tipo:* freemium.

### Telegram
- **Lyzem** (Telegram/Telegraph indexado), **Telegago** (búsqueda Google de t.me), **Telegram Phone Number Checker (Bellingcat)**, **TGStat** (estadísticas de canales), **Osintly**, **Funstat** (media). API vía my.telegram.org. *Tipo:* gratis/freemium.

### LinkedIn
- **CrossLinked** (perfil + conexiones), **RocketReach**, **Hunter.io**, **Apollo** (freemium); búsqueda manual de empleos/ubicación. *Tipo:* gratis/freemium; ToS restrictivo.

### Reddit
- Tras el cierre de Pushshift: **Arctic Shift**, **PullPush**, **Reveddit** (comentarios borrados), dumps históricos; **Reddit search** nativo. *Tipo:* gratis. *Reto:* API oficial de pago y fin de RSS (nov-2026).

### Multi-plataforma / generales
- **Sherlock, Maigret, WhatsMyName, Social Analyzer, Social-Searcher** (monitorización multired con alertas), **Maltego** (link analysis), **ShadowDragon Horizon** (600+ fuentes, pago). Directorios: **OSINT Tools Library** (osintnewsletter), **The OSINT Rack**, **OSINT Combine**, **OSINT Framework**.

**Retos transversales:** APIs cerradas/de pago; scraping contra ToS; cuentas falsas; verificar fecha de último commit; correlación usuario↔persona es inferencia, no prueba. *Fuentes:* tools.osintnewsletter.com, think-pol.com, medium (App CyberYozh), hackread.com.

---

## 8. OSINT de documentos y metadatos avanzados

| Herramienta | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| ExifTool (Phil Harvey) | Lee/escribe/borra metadatos de casi cualquier formato (imagen, PDF, Office, vídeo, audio); GPS, timestamps, dispositivo, software | Gratis/open source | Estándar forense; CLI + librería Perl |
| exif.tools / Exif Info (exifinfo.org) / Metadata2Go / Jimpl | Visores web de EXIF/XMP/IPTC/ICC + hashes + magic bytes | Gratis | Análisis rápido sin instalar; privacidad en navegador |
| pdf-parser / pdfid (Didier Stevens) | Estructura y metadatos de PDF, objetos, autores | Gratis | PDFs: autor, productor, fechas, incremental updates |
| Forensicosint Image Metadata Analyzer | EXIF/GPS/XMP + reporte PDF con hash y metodología | Gratis | Reportes con cadena de custodia |
| GeoSetter / ExifPurge / MetaClean | Geotag / borrado de metadatos | Gratis/freemium | Verificar y sanear |
| FOCA / Metadata Assistant | Extracción masiva de metadatos de documentos | Freemium | Enumeración documental |
| Hugin | Corrección de distorsión/panoramas (fotogrametría) | Gratis | Geometría angular correcta antes de medir sombras |
| Wayback Machine / archive.today | Versiones históricas de documentos/páginas | Gratis | Procedencia temporal |
| Google Pinpoint / Trint / oTranscribe | Transcripción y extracción de texto | Freemium | Escalar análisis de audio/PDF |

**Técnicas:** extraer autor/empresa/fechas/rutas de impresión; detectar *tracked changes*; hashes (MD5/SHA) para integridad; *magic bytes* para tipo real; correlación de metadatos con GEOINT; borrar metadatos antes de publicar (defensa). **Retos:** plataformas borran EXIF al subir; metadatos falsificables; PDFs con actualizaciones incrementales ocultas. *Fuentes:* shadowdragon.io, exiftool.org, hackers-arise.com, osintteam.blog.

---

## 9. OSINT de infraestructura y threat intelligence (CTI) básico

| Herramienta | Qué hace | Tipo | Por qué sirve |
|---|---|---|---|
| Shodan | Buscador de servicios/dispositivos expuestos (puertos, banners, SSL) | Freemium | Superficie de ataque; pivotar IP→infraestructura |
| Shodan InternetDB | API gratuita (puertos, CPE, CVEs) sin clave | Gratis | Enriquecimiento masivo de IP |
| Censys | Inteligencia de infraestructura internet-wide, certificados | Freemium/pago | Activos, posture, certificados |
| VirusTotal | Análisis archivo/URL/dominio/IP multi-motor; passive DNS, WHOIS, SSL | Freemium (API pública no comercial) | Contexto de indicadores; conexiones malware |
| SecurityTrails | DNS/WHOIS histórico, subdominios | Freemium | Evolución de infraestructura; typosquatting |
| crt.sh | Búsqueda en Certificate Transparency (subdominios por certificado) | Gratis | Enumeración pasiva de subdominios |
| urlscan.io | Escaneos de URL, DOM, certificados, screenshots | Freemium | Análisis de phishing/infraestructura |
| GreyNoise | Contexto de ruido de fondo / IPs benignas vs. maliciosas | Freemium | Reducir falsos positivos |
| Intelligence X (intelx.io) | Índice histórico (brechas, dominios, emails) | Freemium/pago | OSINT histórico amplio |
| Maltego | Link analysis visual con conectores | Freemium (Basic gratis, créditos) | Mapear relaciones entidad↔infra |
| SpiderFoot | Recolección OSINT automatizada por módulos | Gratis/open source | Recon configurable |
| theHarvester | Descubrimiento de dominios/emails/hosts | Gratis/open source | Fase inicial de recon |
| OWASP Amass | Enumeración de subdominios/activos | Gratis/open source | Mapa de superficie |
| Mitaka (extensión) | Clic derecho → VT/Shodan/AbuseIPDB/crt.sh | Gratis | Triaje rápido en navegador |
| AbuseIPDB | Reputación de IP | Freemium | Verificar IPs maliciosas |
| MISP / OpenCTI / TheHive | Compartir/gestionar CTI (STIX/TAXII), casos | Gratis/open source | Knowledge graph de IOCs; orquestación |
| AlienVault OTX | Threat exchange comunitario | Freemium | IOCs y pulses |
| Feedly Threat Intel / Recorded Future | Intel de amenazas, CVEs, dark web | Pago | Contexto predictivo |

**Técnicas básicas:** enumeración de subdominios (crt.sh, Amass, subfinder) → fingerprinting (httpx, Shodan) → correlación de certificados/passive DNS → reputación (VT, AbuseIPDB, GreyNoise) → mapeo (Maltego) → gestión (OpenCTI/MISP). Marcos: MITRE ATT&CK, STIX/TAXII, Zero Trust. **Retos/legal:** recopilar solo activos propios o autorizados; verificar fechas de observación (Shodan muestra histórico); API pública de VT no para uso comercial; disturbios de rate-limits. *Fuentes:* foresiet.com, socradar.io, dataimpulse.com, shadowdragon.io, stellarcyber.ai, medium (Certificate Transparency).

---

## Fuentes generales / directorios
- Bellingcat Online Open Source Investigation Toolkit — bellingcat.com
- OSINT Tools Library (OSINT Newsletter) — tools.osintnewsletter.com
- OSINT Framework — osintframework.com
- The OSINT Rack — osintrack.com
- OSINT Combine — osintcombine.com
- CITP Princeton "Holding The Line" (ago-2026) — citp.princeton.edu
- CIRS 2026 Video Verification — aofirs.org
- Global Investigative Journalism Network (GIJN) — gijn.org
- Henk van Ess "Digital Digging"; Tom Vaillant OSINT dataset (Hugging Face)

## Advertencias legales/éticas (transversales)
- GDPR / bases legítimas; Telephone Records and Privacy Protection Act (US, pretexting).
- Reconocimiento facial y geolocalización de personas: riesgo de acoso; interés público y minimización.
- ToS de plataformas y scraping; APIs de pago.
- Todo resultado es **una pista, no un veredicto**; documentar cadena de evidencia reproducible (URL, fecha, hash, metodología).
- Verificar precios/estado de cada herramienta antes de operar: cambian con frecuencia.