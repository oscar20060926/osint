# Informe OSINT 2026 — Ranking Unificado de las Mejores Herramientas

> Consolidado de 3 investigaciones (web, aplicaciones descargables, terminal/CLI).
> Fecha de referencia: noviembre 2026. Precios, cobertura y "stars" cambian con el tiempo: verifica siempre en la fuente oficial.

---

## 🏆 HALL OF FAME — Las 10 mejores OSINT de cualquier tipo

| # | Herramienta | Tipo | Para qué es imprescindible |
|---|-------------|------|----------------------------|
| 1 | **Google Earth Pro / Lens** | App + Web | Geolocalización e imagen inversa. Base de toda investigación visual. |
| 2 | **Maltego** | App (GUI) | Link analysis y grafos de relaciones. Estándar de la industria. |
| 3 | **Sherlock / Maigret** | CLI | Enumeración de usuarios en cientos/miles de sitios. |
| 4 | **SpiderFoot** | App + CLI | Framework OSINT todo-en-uno con correlación automática. |
| 5 | **Shodan / Censys** | Web | Superficie de ataque global (dispositivos, puertos, banners). |
| 6 | **Have I Been Pwned** | Web | Brechas y filtraciones de forma ética y gratuita. |
| 7 | **theHarvester / Amass / Subfinder** | CLI | Recon de dominios, subdominios y emails. |
| 8 | **ExifTool** | CLI + App | Metadatos forenses de referencia (GPS, cámara, fechas). |
| 9 | **Wayback Machine** | Web | Snapshots históricos y preservación de evidencia. |
| 10 | **Hunchly / Autopsy** | App | Captura con cadena de custodia y forense de disco. |

---

## 1️⃣ HERRAMIENTAS WEB (navegador, sin instalar)

**Top 10:** Google Lens · Have I Been Pwned · Shodan · Wayback Machine · TinEye · Yandex Images · WhatsMyName · Google Earth · crt.sh · SunCalc.

**Categorías clave:**
- **Personas/usernames:** WhatsMyName, FreeUsername, Namechk, OSINTsearch, Fingerprint.to.
- **Imágenes inversas/rostros:** Google Lens, Yandex, TinEye, PimEyes (muy sensible legalmente), FotoForensics.
- **Redes sociales (SOCMINT):** Social Searcher, Telegago, TGStat, Maltego.
- **Filtraciones:** HIBP, LeakCheck, DeHashed, Intelligence X, Hudson Rock.
- **Geolocalización:** Google Earth, SunCalc, Sentinel Hub, Mapillary, GeoHints, Flightradar24.
- **Dominios/infraestructura:** crt.sh, Shodan, Censys, DNSDumpster, SecurityTrails, urlscan.io, BuiltWith, VirusTotal.
- **Metadatos:** ExifMeta, exif.tools (100% cliente), MetadataKit, FotoForensics.
- **Directorios:** OSINT Navigator (7.500+ herramientas), OSINT4ALL, Bellingcat Toolkit, Awesome OSINT.

## 2️⃣ APLICACIONES DESCARGABLES (GUI escritorio/móvil)

**Top 10:** Maltego Graph · Google Earth Pro · SpiderFoot · Hunchly · Autopsy · Gephi · ExifTool GUI/Metadata++/GeoSetter · FTK Imager · Cytoscape · IBM i2 Analyst's Notebook.

**Categorías clave:**
- **Link analysis:** Maltego, IBM i2, Lampyre.
- **Forense/adquisición:** Autopsy, FTK Imager, SIFT Workstation, Eric Zimmerman Tools, Volatility 3, Wireshark.
- **Grafos:** Gephi, Cytoscape, NodeXL, Neo4j+Bloom, yEd.
- **Móviles:** Ferret OSINT (Android/iOS), Maigret, Sherlock-OSINT (iOS), OSINT Researcher (iOS).
- **GeoINT con IA:** Raven (antes GeoSpy).

## 3️⃣ HERRAMIENTAS DE TERMINAL / CLI

**Top 10:** Sherlock · Maigret · BBOT · theHarvester · SpiderFoot · Amass · Subfinder · Recon-ng · Holehe · ExifTool.

**Categorías clave:**
- **Usernames:** Sherlock (`pipx install sherlock-project`), Maigret (`pip3 install maigret`), Holehe (email), WhatsMyName (dataset).
- **Subdominios:** Subfinder (pasivo, el más rápido), Amass (OWASP), Sublist3r, BBOT.
- **Infra/emails:** theHarvester, Recon-ng.
- **Frameworks:** SpiderFoot, BBOT (80+ módulos), Recon-ng.
- **Redes/scraping:** Instaloader, Toutatis, Osintgram, xint (alternativa moderna a TWINT).
- **CTI:** vt-cli (VirusTotal), AbuseIPDB/urlscan CLI.

**Flujo CLI recomendado:**
```
maigret usuario → sherlock usuario → holehe correo@dominio.com
subfinder -d dominio.com → amass enum -passive -d dominio.com → theHarvester -d dominio.com -b all
bbot -t dominio.com -f subdomain-enum
exiftool -r -json ./descargas > metadata.json
```

---

## ⚖️ Uso responsable y legal (resumen)
- El OSINT es legal; la frontera es el **acceso no autorizado** (CFAA), el doxxing, el acoso y el spyware sin consentimiento.
- **GDPR/CCPA:** procesar datos personales (aunque sean públicos) exige base jurídica, minimización y finalidad.
- **Brechas:** comprobar tu exposición es legítimo; descargar dumps o usar credenciales filtradas es delito.
- **Reconocimiento facial** (PimEyes, Clearview): categoría especial de datos, alto riesgo regulatorio.
- **OPSEC:** no subas material sensible a terceros; usa infraestructura no atribuible.
- **Evidencia:** preserva con hash (Hunchly), Wayback Machine, Auto Archiver; protocolos NIST SP 800-86 / Berkeley.
- **Autorización por escrito** para pentesting/ASM sobre activos ajenos.

---
*Informe defensivo/periodístico. Verifica precios y disponibilidad en las webs oficiales.*