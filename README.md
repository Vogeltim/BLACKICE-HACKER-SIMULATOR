[README.md](https://github.com/user-attachments/files/32919225/README.md)
<div align="center">

# ▚ BLACKICE // HACKER SIMULATOR

**Egal was du tippst — es wird eine Hack-Sequenz daraus.**
Ein eDEX-UI-inspiriertes Hacking-Spiel als einzelne Windows-EXE. Ohne Setup, ohne Abhängigkeiten, offline spielbar.

![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11-0078D4?logo=windows11&logoColor=white)
![Version](https://img.shields.io/badge/version-1.3.1-19ff6a)
![Size](https://img.shields.io/badge/einzelne%20EXE-84%20MB-ffb300)
![Runtime](https://img.shields.io/badge/runtime-WebView2-00ffd5)
![License](https://img.shields.io/badge/license-MIT-ff2d55)

*Dein Terminal. Dein Netz. Deine Legende.*

</div>

---

> [!IMPORTANT]
> **BLACKICE ist ein Spiel.** Es simuliert Hacking komplett fiktiv — es werden keine echten Systeme, Netze oder Personen angegriffen, kontaktiert oder verletzt. Alle IPs, "Exploits" und Ausgaben sind Zufalls-Text. Für Lacher, nicht für Straftaten. 😉

## 📥 Download & Start

1. Gehe zu **[Releases](../../releases)** und lade `BLACKICE.exe` (84 MB) aus dem aktuellen Release
2. Doppelklicken. Fertig.
3. Tippe irgendwas. Drücke Enter. Willkommen im Netz.

- ✅ Keine Installation, keine Runtime zum Nachladen (WebView2 ist in Windows 10/11 integriert)
- ✅ Läuft komplett offline
- ✅ Auto-Save inklusive — siehe [unten](#-autosave)
- ℹ️ SmartScreen meldet sich beim ersten Start möglicherweise (unsignierte EXE) → *„Weitere Informationen" → „Trotzdem ausführen"*

## 🎮 Spielprinzip

**Jede Eingabe ist ein Hack.** Wirklich jedes. Was du eintippst, wird zum Ziel-Server-„Namen" — der Rest ist inszenierte Hack-Sequenz mit Handshake, Portscan, Exploit, Root-Shell und Beute.

Ein paar Wörter lösen Spezial-Missionen aus:

| Eingabe | Mission |
|---|---|
| *(alles andere)* | Standard-Deep-Hack auf dein Ziel — **8 Phasen lang** (siehe unten) |
| `crack` / `passwort` / `hash` | Passwort-Bruteforce mit Hydra & Hashcat (inkl. Hashcat-Regelwerk & Password-Reuse-Pivot) |
| `wlan` / `wifi` / `router` | WLAN-Penetration: Kanal-Scan → Deauth → Handshake → Aircrack → MITM |
| `phish` / `social` / `anruf` | Social Engineering: OSINT → simuliertes Telefonat → MFA-Fatigue |
| `crypto` / `bitcoin` / `wallet` | Blockchain-Deanon, Contract-Reverse-Engineering & Drain mit Wash-Chain |
| *Zahl oder MAC* | nmap-Deep-Scan mit Service-Bannern, OS-Fingerprint & Vuln-Scripts |
| `burn` | Spuren löschen → Trace-Anzeige auf 0 |
| `reset` | ⚠ Spielstand komplett löschen (neue Identität) |
| `help` / `hilfe` | das in-game Handbuch |

### Systems

- **🕵️ Realistische Lang-Hacks (neu in 1.3)** — der Standard-Hack ist eine komplette Operation in **10 Phasen mit Echtzeit-Op-Uhr** (~150 Sekunden, wie ein echter Pentest-Bericht): Recon (traceroute -A, whois, Shodan) → DNS-Enumeration (dig/dnsrecon, SPF/DMARC) → nmap -A (Original-Transkript mit Service-Versionen & OS-Fingerprint) → CVE-Matching + nuclei-Template-Scans → Web-App/SQLi (sqlmap mit DB-Dump-Tabellen, Hashcat) → Meterpreter-Exploit (4 Payload-Stages, sysinfo/getuid) → Privilege Escalation (linpeas, Kernel-LPE, uid=0) → Lateral Movement (secretsdump, PsExec, krbtgt) → Exfiltration über dnscat2-DNS-Tunnel → Log-Wipe. **weiter tippen lohnt sich**: die Queue nimmt bis zu 4 Befehle vorweg
- **⚡ Trace-System** — Zu oft hacken und die Anzeige läuft voll → **Trace-Minispiel**: 12 Tasten in 8 Sekunden hämmern oder S.W.A.T. metaphorisch vor deiner Tür steht (Strafe: -50 ¢, halbe XP)
- **📈 Progression** — XP, 8 Ränge (Script Kiddie → *„Legende — Verboten"*), ¢-Loot, 9 Achievements, Missionsliste
- **🖥️ eDEX-UI-Vibes** — Live-Node-Feed, Traffic-Graph, System-Last, Threat-Meter, News-Ticker, Boot-Sequenz, Scanlines, Glitch-Effekte, WebAudio-Sounds (null Audiodateien)
- **🎬 Hintergrundvideo** — eigenes „Hackersimulator"-Video hinter dem Terminal, mit Matrix-Rain als Fallback
- **🎵 Terminal-Ambience** — der Terminal-Sound läuft **synchron zum Hintergrundvideo** (Pause/Play/Ende), dazu Boot-Stinger, Trace-Alarm und Error-FX; Mute bleibt gespeichert

## 💾 Auto-Save

Der Spielstand (**XP, Rang, ¢, Achievements, Statistiken**) speichert sich automatisch nach jedem Hack, Level-Up und Achievement.

- Gespeichert wird nach dem Schließen in **`.storage/blackice_save.neustorage` neben der EXE**
- **Spielstand mitnehmen** = EXE + `.storage`-Ordner zusammen kopieren
- Der Save wird beim Start **niemals** durch einen leeren Stand überschrieben (Schreib-Schutz)
- Im Browser-Build gilt dasselbe via localStorage

## 🛠️ Selbst bauen

```bash
# 1. Node.js (LTS) installieren — oder portable Version nutzen
# 2. Projekt klonen
git clone https://github.com/<DEIN-NAME>/blackice-hacker-simulator.git
cd blackice-hacker-simulator

# 3. Neutralino CLI + Binaries
npm install -g @neutralinojs/neu
cd app-src
neu update

# 4. Single-File-EXE mit eingebetteten Ressourcen bauen
neu build --release --embed-resources
# → dist/BLACKICE/BLACKICE-win_x64.exe
```

Der Quellcode liegt komplett in [`app-src/`](app-src/) — kein Framework, kein Build-Step davor: `index.html`, `style.css`, `game.js`, fertig.

## 📁 Projektstruktur

```
├── BLACKICE.exe          # Spielbare Single-File-EXE (aus dem Release laden)
├── app-src/
│   ├── index.html        # Layout: Terminal, HUD, Overlays
│   ├── style.css         # Cyberpunk-Look (Scanlines, Glitch, CRT)
│   ├── game.js           # Spiel-Logik (Hacks, Trace, XP, Save, Audio)
│   ├── js/neutralino.js  # Neutralino-Client-Library
│   ├── sounds/           # Terminal-Loop, Boot-Stinger, Error-FX, Trace-Alarm
│   └── Hackersimulator background.mp4
└── RELEASE_NOTES.md      # Release-Text
```

## 🧰 Tech-Stack

| | |
|---|---|
| **Runtime** | [Neutralino.js](https://neutralino.js.org) v6.9 — 2,4 MB Native-Shell statt 200 MB Electron |
| **Renderer** | Windows WebView2 (Edge/Chromium, in Windows integriert) |
| **Frontend** | Vanilla HTML/CSS/JS — kein Framework, keine Dependencies |
| **Audio** | WebAudio-API (prozedural generierte Sounds) |
| **Packaging** | `neu build --release --embed-resources` → eine EXE, alles drin |

## 📜 Lizenz

[MIT](LICENSE) — mach damit, was du willst.

<div align="center">

**Wenn dir das Spiel gefällt, lass einen ⭐ im Repo da.**

*„regel #1: es gibt keine regeln. tipp einfach los."*

</div>
