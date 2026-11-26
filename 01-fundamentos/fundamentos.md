# Fundamentos y Metodologías OSINT

## Ciclo OSINT (6 pasos, Berkeley Protocol)
1. Online inquiries → 2. Preliminary assessment → 3. Collection → 4. Preservation → 5. Verification → 6. Investigative analysis.

## Frameworks clave
- **Berkeley Protocol (OHCHR + UC Berkeley):** estándares mínimos para identificar, recolectar, preservar, verificar y analizar; evidencia admisible; distingue credibilidad/fiabilidad/veracidad; minimización tipo GDPR.
- **ACH (Analysis of Competing Hypotheses, Heuer/CIA):** refuta hipótesis con matriz evidencia×hipótesis; reduce sesgo de confirmación; gana la hipótesis con menos evidencia en contra.
- **Ciclo de Inteligencia:** planificación → recolección → procesamiento → análisis → difusión (+ retroalimentación).
- **Cyber Kill Chain (recon):** mapea infraestructura del adversario; conecta OSINT con CTI.
- Complementarios: SIFT, Lateral Reading, TCPED, ABCDE (desinformación).

## Verificación y falsos positivos (resumen)
- Ningún detector automático prueba autenticidad; la detección es probabilística.
- Triangulación (≥3 fuentes), SIFT (Stop/Investigate/Find/Trace), Lateral Reading.
- Reverse image con ≥2 motores (Google/Yandex/TinEye/Bing, InVID-WeVerify).
- Metadatos (ExifTool, Amnesty YouTube DataViewer).
- Deepfakes: multi-señal (metadatos + artefactos + reverse + ≥2 detectores + C2PA).
- Cronolocalización (SunCalc, Shadow Finder) y geolocalización (Google Earth, Sentinel).

## IA/LLM y automatización
- MCP servers OSINT (awesome-osint-mcp-servers; osint-toolbox-mcp, frishtik, etc.).
- Agentes autónomos (OpenOSINT, SYNINT, ARES, osint-agent) — colectores deterministas + revisión humana.
- LLMs locales (Ollama con loopback, LM Studio, llama.cpp) — fijar `OLLAMA_HOST=127.0.0.1`.
- Python: requests/httpx, BeautifulSoup/Scrapy, ExifRead, ipwhois, dnspython, networkx, phonenumbers, suncalc.

## Preservación de evidencia
- Estándares: SWGDE 18-F-002 v2.0, NIST IR 8387, Berkeley Protocol, Convenio de Budapest, C2PA 2.4.
- Herramientas: Hunchly, Wayback/archive.today, c2patool, ExifTool, sha256sum.
- Formato: SHA-256 + segundo algoritmo, EXIF/XMP, Content Credentials, registro con ID/fecha/transferencias.

## Relacionados
- [[tecnicas-y-verificacion]] (en 03-tecnicas)
- [[verticales]] (en 05-especializado)