# OPSEC, Anonimato y Dark Web para Investigadores OSINT

> Fecha de referencia: noviembre 2026. Precios/licencias cambian: verificar en fuente oficial.
> Nada de esto sustituye asesoría legal ni autorización judicial/corporativa.

## 1. OPSEC para investigadores

### Conceptos
- **Anonimato:** sin vínculo entre actividad e identidad real (exigente y frágil).
- **Seudonimato:** identidad ficticia estable (sock puppet); no es anonimato.
- **Compartimentación:** separar identidades, dispositivos, redes, cuentas y casos.
- **Higiene digital:** limpieza de cookies, caché, metadatos, DNS, huellas.
- **Huella del investigador:** IP, user-agent, zona horaria, idioma, horarios, estilo, referrer, metadatos, extensiones.

### Proceso OPSEC (5 pasos)
1. Información crítica (qué te delata).
2. Amenazas (quién puede detectarte).
3. Vulnerabilidades (hábitos/herramientas).
4. Análisis de riesgo (probabilidad × impacto).
5. Contramedidas (VMs desechables, VPN/Tor, navegadores endurecidos, identidades separadas, cifrado).

### Señales que revelas sin querer
IP pública, user-agent/huella, cookies/trackers, DNS, metadatos (EXIF/PDF/Office), referrer, WebRTC, canvas/WebGL/fuentes, comportamiento/horarios, cuentas personales.

### Errores frecuentes
Entrar en cuentas personales desde el entorno de investigación; reutilizar seudónimo; mezclar dispositivo/red; ignorar metadatos; no controlar estilo/horarios; extensiones sin revisar; creer que VPN/Tor arreglan mal OPSEC. Casos: Ross Ulbricht (Silk Road), Alexandre Cazes (AlphaBay).

### Sock puppets
Correo/usuario únicos, backstory coherente, huella de navegador/sistema consistente, nunca acceso desde red/dispositivo real, no reutilizar fotos/idioma/muletillas, guardar en KeePassXC/Bitwarden.

### Checklist mínimo
- [ ] Dispositivo/VM desechable por caso.
- [ ] Red distinta (VPN sin logs + Tor cuando aplique).
- [ ] Navegador endurecido y perfil separado.
- [ ] Cuentas/correos exclusivos.
- [ ] Sin metadatos en lo que publicas.
- [ ] Comunicación cifrada (Signal/Session/Element, ProtonMail/Tutanota, PGP).
- [ ] Registro de herramienta/identidad/horario.
- [ ] Revisar permisos de extensiones y fugas (IP/DNS/WebRTC).
- [ ] Plan de "qué hago si me detectan".

## 2. Herramientas de anonimato

| Herramienta | Qué hace | Tipo | Por qué |
|---|---|---|---|
| Tor Browser | Firefox endurecido + red Tor | Gratis, OSS | Anonimato de referencia; acceso onion |
| Tails | SO live amnésico; todo por Tor | Gratis, OSS | No dejar rastro; portátil |
| Whonix | Gateway + Workstation Tor | Gratis, OSS | Evita fugas IP/DNS; persistente |
| Qubes OS | Compartimentación por qubes (Xen) | Gratis, OSS | Separación fuerte; base Qubes-Whonix |

**Regla:** Tails = entrar/hacer/desaparecer; Whonix/Qubes = persistente; Tor Browser = rápido; VPN = ocultar IP al ISP (no anonimato fuerte por sí sola).

### VPNs
- **Mullvad** (~5 €/mes, cuenta numérica, sin email, pagos Monero/efectivo) — estándar de mínima retención.
- **IVPN** (sin email, auditorías) — alternativa pequeña.
- **Proton VPN** (open source, no-logs, plan gratis) — mejor equilibrio.
- **Windscribe** (10 GB gratis, ofuscación) — económica.
- Cautela: VPN no sustituye Tor; evitar VPNs gratis desconocidas.

### Navegadores
- **Tor Browser** (anonimato/onion) · **Mullvad Browser** (anti-huella con VPN) · **LibreWolf** (Firefox sin telemetría) · **Brave** (Shields + ventana Tor) · **Firefox + hardening** (resistFingerprinting, HTTPS-Only, contenedores).

### Extensiones de privacidad
uBlock Origin, NoScript, Privacy Badger, Cookie AutoDelete, Canvas Fingerprint Defender, Chaff, ClearURLs, Decentraleyes, Location Guard, Multi-Account Containers, User-Agent Switcher.
> HTTPS Everywhere archivado; usar modo HTTPS-Only nativo.

### Combinación por modelo de amenaza
- Bajo: navegador endurecido + uBlock + VPN.
- Medio: VM dedicada + VPN sin logs + LibreWolf/Mullvad + contenedores.
- Alto: Tails/Whonix/Qubes + Tor + cuentas desechables + cifrado + vault offline.
- Muy alto: Qubes-Whonix + desechables + hardware token + copias cifradas + protocolo de detección.

## 3. Extensiones de navegador para OSINT

### Pivoteo de artefactos
Mitaka (clic derecho → VT/urlscan/Censys/Shodan, "refang"), Sputnik, Gotanda, ThreatPinch Lookup, Pulsedive, OSIRIS, Vulners Web Scanner.

### Captura/preservación
Hunchly (pago, evidencia defendible), Vortimo (entidades+enlaces), Wayback Machine, Go Back in Time, Web Archives, Web Cache Viewer, FireShot, Nimbus, Save Page WE, Distill Web Monitor, Visualping, Page Monitor, Fetcher.

### Infraestructura/hosting
Wappalyzer, BuiltWith, DNSlytics, Shodan, ZoomEye/FOFA, Scan WP, Netcraft, IP/Domain Info, OpenLink Structured Data Sniffer, Link Gopher, Linkclump.

### Personas/correos
Hunter Email Finder, Email Extract, L.O.C (Facebook), Return YouTube Comment Username.

### Imagen/vídeo/verificación
Search by Image (30+ motores), TinEye, EXIF Viewer Pro, PhotOSINT, InVID-WeVerify, Fake Profile Detector, Resemble AI Deepfake Detector, Screenshot YouTube, Image Downloader.

### Scraping ligero
Instant Data Scraper, Data Scraper, Simplescraper, CrowdScrape, FOCA Files Finder.

> Kit equilibrado: Mitaka + Wappalyzer/DNSlytics + Vortimo/Hunchly + Multi-Account Containers. No acumular docenas: cada extensión ve todo lo que visitas.

## 4. Dark web / onion

### Herramientas
- **Tor Browser** (puerta de entrada) · **Tails/Whonix** (contención).
- **Ahmia** (buscador onion desde surface, filtra abuso) · **Torch** (onion nativo, más amplio).
- **OnionSearch** (CLI, multi-motor vía Tor, CSV) · **AIL Framework** (recolección/correlación) · **VoidAccess** (self-hosted, Docker, grafo) · **OnionScan** (escáner técnico).
- Comerciales: **DarkOwl Vision**, **Flare**, **Recorded Future**, **IntelX**, **HIBP**, **Telemetry** (Telegram), **Ransomware.live**.

### Precauciones
Nunca red/cuenta/dispositivo real; desactivar JS/WebRTC/descargas; VM desechable/Tails; no interactuar/comprar/publicar; distinguir OSINT de DARKInt; documentar URL onion + fecha UTC + hash + captura; verificar autenticidad (honeypots/estafas); considerar monitorización comercial.

## 5. Rastreo de criptomonedas

### Técnicas
Clustering heurístico, etiquetado de entidades, trazado multi-salto/cross-chain, demixing, pivote off-chain, análisis temporal/flujo, scoring de riesgo.

### Comerciales
Chainalysis Reactor, TRM Labs Forensics, Elliptic Investigator, Crystal Intelligence, CipherTrace (Mastercard), Allium.

### Gratuitos/freemium
Blockchain.com Explorer, Etherscan, Blockchair, mempool.space, Arkham, MetaSleuth, Breadcrumbs, WalletExplorer, Chainabuse, Bitcoin Who's Who, Dune.

> Límite: la cadena muestra el dinero, no la persona. La identidad llega por off-chain (KYC, foros, reutilización de alias, metadatos).

## 6. Gestión de secretos y aislamiento

- **Secretos:** KeePassXC (offline, KDBX, YubiKey), Bitwarden/Vaultwarden (self-host), VeraCrypt, LUKS/cryptsetup, YubiKey.
- **Aislamiento:** Qubes OS, Whonix, Tails, VirtualBox/VMware/KVM (snapshots), Docker/Podman (contenedores desechables), Firefox Multi-Account Containers.
- **Arquitectura:** vault offline (KeePassXC sin red + YubiKey); VM dedicada por caso; anonimato en Qubes-Whonix/Tails separado; desechable para enlaces no confiables; secretos en KeePassXC/Bitwarden; backups cifrados probados.

## 7. Conclusión operativa
El OPSEC es un sistema (compartimentación + anonimato + higiene + disciplina), no una herramienta. Anonimato fuerte = Tails/Whonix/Qubes + Tor + cuentas desechables. Seudonimato = personas únicas + huella consistente + nunca red real. Pocas extensiones oficiales. Dark web = entorno aislado sin interacción. Cripto = analytics + exploradores + pivote off-chain. Legalidad y ética: autorización, proporcionalidad, protección de datos, cadena de custodia.

## Fuentes
SOS Intelligence · ShadowDragon · Awesome Browser Extensions for OSINT · Tor Project · Tails · Whonix · Qubes OS · Mullvad · IVPN · Proton VPN · Windscribe · EFF Cover Your Tracks · UncovAI · OnionSearch · AIL Framework · VoidAccess · Ahmia · OnionScan · Chainalysis · TRM Labs · Elliptic · Crystal · FaceSeek · Allium · KeePassXC · Bitwarden · VeraCrypt · YubiKey · HackTricks.