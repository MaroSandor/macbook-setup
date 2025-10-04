# MacBook Fejlesztői Környezet - Telepítési Útmutató

## Tartalomjegyzék
1. [Visual Studio Code és Bővítmények](#visual-studio-code-és-bővítmények)
2. [Docker - Alapok és Tanulás](#docker---alapok-és-tanulás)
3. [Safari Webfejlesztéshez](#safari-webfejlesztéshez)
4. [Windows Távoli Elérés](#windows-távoli-elérés)
5. [SQL vs NoSQL - Adatbázis Kliensek](#sql-vs-nosql---adatbázis-kliensek)
6. [Transmission és Torrent Szerverek](#transmission-és-torrent-szerverek)
7. [VirtualBox Alternatívák](#virtualbox-alternatívák-macos-re)
8. [Telepítendő Szoftverek Listája](#telepítendő-szoftverek-listája)

---

## Visual Studio Code és Bővítmények

### Általános, mindenkinek

- **Prettier** - Kódformázás automatikusan
- **ESLint** - JavaScript/TypeScript linter
- **GitLens** - Git szuperképességek (ki, mikor, mit változtatott)
- **Error Lens** - Hibák inline megjelenítése
- **Path Intellisense** - Fájl útvonal auto-complete
- **Auto Rename Tag** - HTML/XML tag párok automatikus átnevezése
- **Bracket Pair Colorizer 2** - Zárójelek színezése (beépült VSCode-ba)
- **indent-rainbow** - Behúzások színezése

### Webfejlesztés (Full-Stack)

- **Live Server** - Helyi dev szerver auto-reload-dal
- **REST Client** - API tesztelés VSCode-ból (Postman alternatíva)
- **Thunder Client** - Még egy Postman alternatíva, jobban integrált
- **HTML CSS Support** - CSS class intellisense HTML-ben
- **Auto Close Tag** - HTML tagek automatikus lezárása
- **JavaScript (ES6) code snippets** - Gyors kódrészletek
- **Vetur** vagy **Volar** - ha Vue.js
- **ES7+ React/Redux/React-Native snippets** - ha React
- **Tailwind CSS IntelliSense** - ha Tailwind-et használsz
- **Database Client** - Adatbázisok böngészése VSCode-ból

### Python

- **Python** (Microsoft hivatalos) - KÖTELEZŐ
- **Pylance** - Gyorsabb Python nyelvi szerver
- **Python Indent** - Intelligens behúzás
- **autoDocstring** - Docstring generálás
- **Jupyter** - Notebook támogatás

### Java

- **Extension Pack for Java** (Microsoft) - Csomag, tartalmazza:
  - Language Support for Java
  - Debugger for Java
  - Test Runner for Java
  - Maven for Java
  - Project Manager for Java
  - Visual Studio IntelliCode
- **Spring Boot Extension Pack** - ha Spring-et használsz

### Swift (kiegészítő Xcode mellé)

- **Swift Language** - Swift syntax highlighting
- **SourceKit-LSP** - Language Server Protocol Swift-hez

⚠️ **Vigyázat:** Swift fejlesztéshez az Xcode a király, VSCode csak kiegészítő lehet

### Docker

- **Docker** (Microsoft) - Dockerfile syntax, konténer menedzsment
- **Remote - Containers** - Fejlesztés konténerben

### Egyéb hasznos

- **TODO Highlight** - TODO, FIXME kommentek kiemelése
- **Better Comments** - Színes kommentek
- **Code Spell Checker** - Helyesírás ellenőrzés kódban
- **Material Icon Theme** vagy **VSCode Icons** - Szebb fájl ikonok

---

## Docker - Alapok és Tanulás

### Mi az a Docker?

Röviden: **csomagolod az alkalmazásodat + függőségeit egy "konténerbe"**, ami bárhol ugyanúgy fut. Mint egy könnyű virtuális gép, de gyorsabb és hatékonyabb.

### Miért jó?

- ✅ "Nálam működött" probléma megoldása
- ✅ Gyors környezetek létrehozása (adatbázis, Redis, stb.)
- ✅ Izolált környezetek (nem szennyezi be a géped)
- ✅ Azonos környezet dev/test/production-ben

### Alapfogalmak

**Image (kép):**
- Egy "sablon", amiből konténereket készítesz
- Pl. `nginx:latest`, `python:3.11`, `postgres:15`

**Container (konténer):**
- Egy futó példány az image-ből
- Indítod, leállítod, törlöd

**Dockerfile:**
Recept, hogyan készíts saját image-et

```dockerfile
FROM python:3.11
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

**Docker Compose:**
Több konténer együtt kezelése (pl. frontend + backend + adatbázis)

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: secret
```

### Alapparancsok

```bash
# Konténer futtatása
docker run -d -p 8080:80 nginx

# Futó konténerek listája
docker ps

# Konténer leállítása
docker stop <container_id>

# Image letöltése
docker pull postgres:15

# Konténer törlése
docker rm <container_id>

# Compose projekt indítása
docker-compose up -d

# Compose leállítás
docker-compose down
```

### Gyakorlati példa - PostgreSQL adatbázis

```bash
docker run -d \
  --name my-postgres \
  -e POSTGRES_PASSWORD=mysecret \
  -e POSTGRES_DB=myapp \
  -p 5432:5432 \
  postgres:15
```

Kész! Postgres adatbázis fut `localhost:5432`-n, telepítés nélkül!

### Tanulási források (sorrendben)

1. **Docker hivatalos tutorial** (a legjobb kezdésnek):
   https://docs.docker.com/get-started/

2. **Docker for Beginners** (gyakorlati):
   https://docker-curriculum.com/

3. **Interaktív learning:**
   https://www.katacoda.com/courses/docker

4. **Magyar nyelvű bevezető:**
   https://prog.hu/tudastar/docker

5. **YouTube (vizuális tanuláshoz):**
   - "Docker Tutorial for Beginners" - TechWorld with Nana
   - "Docker Crash Course" - Traversy Media

### Gyakorlati projekt ötlet

Készíts egy egyszerű webappot (pl. Flask/Python), csomagold Docker-be, és futtasd Docker Compose-zal adatbázissal együtt.

---

## Safari Webfejlesztéshez

### Szükséges-e Safari?

**IGEN**, ha iOS/macOS appokat fejlesztesz, vagy komplett cross-browser tesztelést akarsz.

### Piaci részesedés

- 🌍 Globálisan: ~20-25% (második hely Chrome után)
- 🇺🇸 USA-ban: ~30-35%
- 📱 Mobilon: ~25-30% (iOS!)
- 💻 macOS-en: 50%+

### Miért tesztelj Safari-ban

- **WebKit engine különbözik** Chrome-tól (Blink) és Firefox-tól (Gecko)
- **iOS-en KÖTELEZŐ** WebKit (Chrome iOS is WebKit-et használ!)
- **CSS/JS különbségek** lehetnek
- **Mobilos viselkedés** eltérhet

### Safari Developer Tools

Safari → Beállítások → Speciális → "Fejlesztői menü megjelenítése"

Ezután ugyanolyan dev tools mint Chrome, csak Apple-ös dizájnnal.

**Tipp:** Használd **BrowserStack** vagy **LambdaTest** online tesztelésre más böngészőkben/OS-ekben is.

---

## Windows Távoli Elérés

### Legjobb megoldás: Windows App (Microsoft Remote Desktop) ⭐

- ✅ INGYENES
- ✅ Natív macOS app
- ✅ Legjobb teljesítmény RDP-hez
- ✅ **Ez a legjobb választás!**

### Alternatívák

1. **Parallels Client (RAS)**
   - Ha céges környezetben RAS szerver van
   - Jobb mint TeamViewer távoli Windows-hoz

2. **AnyDesk**
   - TeamViewer alternatíva
   - Gyorsabb lehet
   - Ingyenes személyes használatra

3. **Chrome Remote Desktop**
   - Böngészőalapú, cross-platform
   - Egyszerű, de lassabb

4. **RustDesk** (nyílt forráskódú)
   - TeamViewer/AnyDesk alternatíva
   - Self-hosted is lehet
   - Ingyenes

### Vélemény

Maradj a **Windows App**-nál, ez a legjobb RDP kliens macOS-re. Más csak akkor, ha nem RDP-t használ a szerver.

---

## SQL vs NoSQL - Adatbázis Kliensek

### SQL vagy NoSQL?

**Mindkettő!** Más feladatra valók.

### SQL (PostgreSQL, MySQL, MariaDB)

✅ **Használd, ha:**
- Strukturált adatok
- Relációk fontosak (user → posts → comments)
- ACID tranzakciók kellenek
- Komplex lekérdezések (JOIN-ok)
- Pénzügyi, enterprise rendszerek

**Ajánlott:** **PostgreSQL** (modern, powerful, ingyenes)

### NoSQL (MongoDB, Redis, Firestore)

✅ **Használd, ha:**
- Flexibilis séma kell
- Gyors írás/olvasás nagy skálán
- Dokumentum-alapú adatok (JSON-szerű)
- Horizontális skálázhatóság
- Real-time alkalmazások

**Ajánlott:** **MongoDB** (dokumentum DB) vagy **Redis** (cache/session)

### Kell kliens szoftver?

**NEM KÖTELEZŐ**, de **NAGYON HASZNOS!**

**Felhő/remote adatbázishoz is kell?**
**IGEN**, a kliens szoftverek pont távoli adatbázisokhoz csatlakoznak!

### Legjobb kliens szoftverek

#### Univerzális (minden DB-hez)

1. **DBeaver** (INGYENES, nyílt forráskódú) ⭐
   - SQL: Postgres, MySQL, SQLite, Oracle, stb.
   - NoSQL: MongoDB, Cassandra, Redis
   - Vizuális query builder
   - ER diagramok
   - **ERŐSEN AJÁNLOTT!**

2. **TablePlus** (fizetős, de szép)
   - Native macOS app
   - Gyors, modern UI
   - SQL + NoSQL támogatás

#### Csak SQL-hez

- **Sequel Ace** (ingyenes, macOS) - MySQL/MariaDB
- **Postico** (fizetős, macOS) - PostgreSQL
- **pgAdmin** (ingyenes) - PostgreSQL

#### Csak NoSQL-hez

- **MongoDB Compass** (hivatalos, ingyenes)
- **Redis Commander** (web-based)
- **Robo 3T/Studio 3T** - MongoDB

### Docker + DB példa

```bash
# PostgreSQL felhúzása
docker run -d --name postgres -e POSTGRES_PASSWORD=secret -p 5432:5432 postgres:15

# MongoDB felhúzása
docker run -d --name mongo -p 27017:27017 mongo:7

# Redis felhúzása
docker run -d --name redis -p 6379:6379 redis:7
```

Ezután DBeaver-rel csatlakozol `localhost:5432/27017/6379`-re!

### Javaslat

- **Telepíts DBeaver-t** - univerzális, ingyenes, mindent tud
- **Gyakorolj Docker-rel** mindkét DB típussal
- **Tanulj PostgreSQL-t** SQL-hez (modern, erős)
- **Tanulj MongoDB-t** NoSQL-hez (népszerű, jó dokumentáció)

---

## Transmission és Torrent Szerverek

### Mi az a torrent szerver?

Egy gép, ami **24/7 fut**, tölti a torrenteket, és TE egy **webes felületen** vagy **kliens alkalmazásból** menedzseled távról.

### Hogyan működik?

```
┌─────────────┐          ┌──────────────────┐
│  Te (kliens)│ ◄──────► │  Torrent szerver │
│  Böngésző/  │  Webes   │   (seedbox/NAS/  │
│  Transmission│ felület  │    Raspberry Pi) │
└─────────────┘          └──────────────────┘
                                   │
                                   ▼
                            Fájlok tárolása
```

### Torrent szerver megoldások

#### 1. Transmission Daemon (ajánlott kezdőknek)

- Transmission **szerver módban** fut egy gépen
- **Transmission Remote GUI** (kliens app) vagy webes felület
- Ingyenes, nyílt forráskódú

**Telepítés (pl. Raspberry Pi-ra vagy Linux szerverre):**

```bash
sudo apt install transmission-daemon
```

Webes felület: `http://szerver-ip:9091`

**macOS kliens:** **Transmission Remote GUI** - macOS alkalmazás a távoli Transmission menedzseléséhez

#### 2. qBittorrent (webes UI beépítve)

- Teljesen ingyenes
- Szép webes felület
- Könnyű beállítás

**Docker példa:**

```bash
docker run -d \
  --name qbittorrent \
  -p 8080:8080 \
  -p 6881:6881 \
  -v /path/to/downloads:/downloads \
  linuxserver/qbittorrent
```

Webes UI: `http://localhost:8080`

#### 3. Fizetős seedbox szolgáltatások

- **Seedbox.io**, **Whatbox**, **Ultra.cc**
- Havi $5-20
- Gyors internet (100GB-1TB tárhely)
- Előre telepített szoftver
- Csak bejelentkezel és használod

#### 4. Saját szerver (NAS/Raspberry Pi/VPS)

- **Synology/QNAP NAS** - Download Station app
- **Raspberry Pi** - Transmission/qBittorrent
- **VPS (pl. Hetzner, OVH)** - seedbox építés

### Transmission lehet kliens?

**IGEN!** Pontosan ezt csinálja:

- **Transmission** (macOS) = Kliens app
- **Transmission Daemon** (szerver) = Háttérben fut
- **Transmission Web UI** = Böngészős kezelés

### Ajánlás

#### Ha van Raspberry Pi / régi laptop / NAS:

1. Telepíts rá **qBittorrent-nox** (no X, nincs GUI)
2. Érd el webes felületen: `http://ip:8080`
3. Fájlok a szerverre töltődnek
4. Samba/FTP-vel eléred a fájlokat

#### Ha csak egyszerűen akarsz:

1. Vegyél egy **olcsó VPS-t** (Hetzner ~€4/hó, 1TB forgalom)
2. Telepíts **Docker-t** + **qBittorrent**-et
3. Torrentek ott töltődnek
4. SFTP-vel/Nextcloud-dal szinkronizálod

#### Házilag (gyors megoldás):

```bash
# qBittorrent Docker konténer
docker run -d \
  --name qbittorrent \
  -e PUID=1000 -e PGID=1000 \
  -p 8080:8080 -p 6881:6881 \
  -v ~/torrents:/downloads \
  linuxserver/qbittorrent
```

Nyisd meg: `http://localhost:8080`

Alapértelmezett jelszó: `adminadmin` (változtasd meg!)

---

## VirtualBox Alternatívák macOS-re

### Miért érdemes alternatíva?

- VirtualBox macOS-en **lassú** és **bugos** (főleg Apple Silicon-on)
- Jobb alternatívák léteznek

### Alternatívák

#### 1. UTM (INGYENES, nyílt forráskódú) ⭐⭐⭐

- **LEGJOBB INGYENES** macOS-re
- Natív Apple Silicon (M1/M2/M3) támogatás
- QEMU alapú
- Linux, Windows futtatás
- Egyszerű UI

**Telepítés:**

```bash
brew install --cask utm
```

**Előnyök:**
- ✅ Ingyenes
- ✅ Apple Silicon optimalizált
- ✅ Jó teljesítmény
- ✅ Modern UI

**Hátrányok:**
- ❌ Kevesebb funkció mint Parallels/VMware

#### 2. Parallels Desktop (FIZETŐS, ~$99/év) ⭐⭐⭐⭐⭐

- **LEGJOBB macOS-re** (ha fizetsz)
- Natív Apple Silicon
- Blazing fast teljesítmény
- Windows 11 ARM futtatása
- Coherence Mode (Windows appok macOS-ként)
- USB, hálózat, shared folders - minden tökéletesen működik

**Diák kedvezmény:** ~$40/év

**Előnyök:**
- ✅ Legjobb teljesítmény
- ✅ Minden feature
- ✅ Stabil, professzionális

**Hátrányok:**
- ❌ Fizetős (de megéri)

#### 3. VMware Fusion (INGYENES Personal Use!) ⭐⭐⭐⭐

- **INGYENES** lett 2024-ben personal use-ra!
- Jó teljesítmény
- Apple Silicon támogatás
- Professzionális features

**Előnyök:**
- ✅ Ingyenes (personal use)
- ✅ Stabil
- ✅ Jó teljesítmény

**Hátrányok:**
- ❌ Kicsit bonyolultabb mint Parallels

#### 4. Docker (Linux konténerekhez) ⭐⭐⭐⭐⭐

- Ha **csak Linuxot** tesztelsz, **Docker a nyerő**
- Gyorsabb mint VM
- Kevesebb erőforrás
- Modern fejlesztői workflow

**Példa:**

```bash
# Ubuntu konténer
docker run -it ubuntu:22.04 bash

# VS Code Remote Containers-szel fejleszthetsz benne
```

#### 5. Multipass (Ubuntu-hoz) ⭐⭐⭐

- Canonical (Ubuntu készítői) terméke
- Csak Ubuntu VM-ek
- Gyors, egyszerű
- Ingyenes

```bash
brew install multipass
multipass launch --name dev
multipass shell dev
```

### Összehasonlítás

| Megoldás | Ár | Teljesítmény | Egyszerűség | Apple Silicon |
|----------|-------|--------------|-------------|---------------|
| **UTM** | 🆓 Ingyenes | ⭐⭐⭐ | ⭐⭐⭐⭐ | ✅ Natív |
| **Parallels** | 💰 $99/év | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ✅ Natív |
| **VMware Fusion** | 🆓 Ingyenes | ⭐⭐⭐⭐ | ⭐⭐⭐ | ✅ Natív |
| **VirtualBox** | 🆓 Ingyenes | ⭐⭐ | ⭐⭐⭐ | ❌ Nincs |
| **Docker** | 🆓 Ingyenes | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ✅ Natív |

### Javaslat

#### Ha egyetemista vagy (van diák kedvezmény):
→ **Parallels Desktop** (~$40/év) - megéri, hibátlan

#### Ha ingyenest akarsz:
→ **UTM** - modern, jó, Apple Silicon-on is megy

#### Ha csak Linux konténerek kellenek:
→ **Docker** - ez a legjobb, leggyorsabb

#### Ha Windows 11 ARM kell:
→ **Parallels** vagy **VMware Fusion**

#### Ha Ubuntu-val játszol:
→ **Multipass** - gyors, egyszerű

---

## Telepítendő Szoftverek Listája

### Fejlesztői eszközök

```
┌─────────────────────────────────────────┐
│         FEJLESZTŐI KÖRNYEZET            │
├─────────────────────────────────────────┤
│ ✅ Visual Studio Code + bővítmények     │
│ ✅ IntelliJ IDEA (Java/Kotlin)          │
│ ✅ Android Studio (Android)             │
│ ✅ Xcode (iOS/macOS)                    │
│ ✅ JetBrains Toolbox                    │
├─────────────────────────────────────────┤
│ ✅ iTerm2 (Terminal)                    │
│ ✅ GitKraken (Git GUI)                  │
│ ✅ Docker (Konténerek)                  │
│ ✅ Postman (API tesztelés)              │
│ ✅ DBeaver (Adatbázis kliens)           │
│ ✅ SceneBuilder (JavaFX)                │
├─────────────────────────────────────────┤
│         BÖNGÉSZŐK ÉS KOMMUNIKÁCIÓ       │
├─────────────────────────────────────────┤
│ ✅ Safari (Beépített, dev tools)        │
│ ✅ Discord                              │
│ ✅ Messenger                            │
├─────────────────────────────────────────┤
│         PRODUKTIVITÁS                   │
├─────────────────────────────────────────┤
│ ✅ CollaNote (Jegyzetek)                │
│ ✅ One Markdown (Markdown)              │
│ ✅ Microsoft Office 365 csomag          │
│   (Word, Excel, Teams)                  │
├─────────────────────────────────────────┤
│         TÁVOLI HOZZÁFÉRÉS               │
├─────────────────────────────────────────┤
│ ✅ Windows App (RDP)                    │
│ ✅ TeamViewer (Távoli segítség)         │
├─────────────────────────────────────────┤
│         EGYÉB ESZKÖZÖK                  │
├─────────────────────────────────────────┤
│ ✅ Transmission (Torrent)               │
│ ✅ Symbols Explorer (SF Symbols)        │
│ ✅ UTM vagy Parallels (VM)              │
└─────────────────────────────────────────┘
```

### Következő lépések

1. ✅ **Gyári visszaállítás**
2. ✅ **Alaprendszer + fenti appok telepítése**
3. 📚 **Docker tutorial végigcsinálása** (1-2 nap)
4. 🗄️ **DBeaver telepítés + PostgreSQL/MongoDB Docker-rel tesztelés**
5. 🐧 **UTM/Parallels kipróbálás Linux VM-mel**

---

## Hasznos parancsok gyűjteménye

### Homebrew telepítés (ha nincs)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Gyakori telepítések Homebrew-val

```bash
# Alapok
brew install --cask visual-studio-code
brew install --cask iterm2
brew install --cask docker
brew install --cask postman
brew install --cask gitkraken

# Adatbázis kliens
brew install --cask dbeaver-community

# VM
brew install --cask utm
# VAGY
brew install --cask parallels

# JetBrains
brew install --cask jetbrains-toolbox

# Kommunikáció
brew install --cask discord

# Jegyzetek
brew install --cask collanote
```

### Docker Quick Reference

```bash
# Image kezelés
docker pull <image_name>
docker images
docker rmi <image_id>

# Konténer kezelés
docker run -d --name <name> <image>
docker ps
docker ps -a
docker stop <container_id>
docker start <container_id>
docker rm <container_id>

# Logs és inspect
docker logs <container_id>
docker inspect <container_id>

# Takarítás
docker system prune -a
```

---

**Utolsó frissítés:** 2025. október

**Készítette:** Claude AI (Anthropic)
