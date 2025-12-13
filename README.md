# Klipper Multi-Printer Dashboard

Ein leichtgewichtiges **HTML/CSS Dashboard zur gleichzeitigen Überwachung mehrerer Klipper‑Drucker** – ähnlich einer Videoüberwachung.

Optimiert für **Mainsail / Klipper API**, mehrere Kamerastreams und schnelle Notfall‑Aktionen.

---

## 🚀 Features

* 📹 Live-Webcam je Drucker (MJPEG)
* 🔍 Fullscreen-Modus per Klick
* 📊 Live-Status (Printing / Paused / Error / Offline)
* ⏱ Fortschritt & Restzeit
* 🔥 Nozzle- & Bed-Temperaturen inkl. Setzen
* 🎯 Speed / Flow / Fan Anzeige
* 🧯 Emergency Stop (pro Drucker)
* 🔔 Browser Notifications & Alarm-Sound bei kritischen Fehlern
* 💾 Drucker & Namen persistent via LocalStorage
* 🎨 TailwindCSS (CDN, kein Build)

---

## 📁 Repository Struktur

Dieses Projekt ist **bewusst als Single-File-Dashboard** umgesetzt (einfach deployen, kein Build-Tool).

```
klipper-multi-dashboard/
│
├── index.html              # Komplettes Dashboard (HTML + CSS + JS)
├── README.md               # Dokumentation
│
└── assets/
    └── screenshots/        # Optional: Screenshots fürs README
```

klipper-multi-dashboard/
│
├── index.html              # Haupt-Dashboard
├── config.js               # Drucker & Kamera Konfiguration
├── README.md               # Dokumentation
│
├── css/
│   ├── style.css           # Layout & Grid
│   ├── cards.css           # Drucker-Karten
│   └── status.css          # Farben (printing / error / idle)
│
├── js/
│   ├── api.js              # Klipper API Calls
│   ├── dashboard.js        # Rendering & Logik
│   ├── actions.js          # Pause / Resume / Cancel
│   └── utils.js            # Helferfunktionen
│
└── assets/
├── icons/
└── screenshots/

````

---

## ⚙️ Konfiguration

Die Drucker werden **dynamisch über die UI hinzugefügt** und im `localStorage` gespeichert.

- ➕ Drucker hinzufügen per IP:Port (z. B. `192.168.188.107:7125`)
- ✏️ Druckernamen direkt im Dashboard editierbar
- 💾 Persistenz über Browser-Neustarts

➡️ **Kein externes Config-File nötig**.

---

## 🔌 Verwendete Klipper Endpoints

- `/printer/objects/query`
  - `heater_bed`
  - `extruder`
  - `print_stats`
  - `display_status`
  - `webhooks`
  - `toolhead`
  - `gcode_move`
  - `fan`

- `/printer/print/pause`
- `/printer/print/resume`
- `/printer/print/cancel`
- `/printer/print/start`
- `/printer/gcode/script`
- `/printer/emergency_stop`

---

## 🧯 Sicherheitshinweis

Dieses Dashboard erlaubt **kritische Steuerbefehle**.

➡️ **Nur im lokalen Netzwerk betreiben** oder per Auth / Reverse Proxy absichern.

---

## 🛣 Roadmap

- [ ] Fullscreen Kamera-Modus
- [ ] Globaler Panic‑Button
- [ ] Browser Notifications bei Fehlern
- [ ] Drucker‑Health (Stunden, Wartung)
- [ ] Obico / KI‑Fehlererkennung (optional)

---

## 📸 Screenshots

> Coming soon

---

## 🛠 Installation

Dieses Dashboard benötigt **keine Installation, keinen Webserver und keine Build-Tools**.

### ✅ Voraussetzungen
- Klipper mit **Moonraker**
- Webcams erreichbar (MJPEG)
- Browser im **gleichen Netzwerk** wie die Drucker

---

### 📄 Schritt 1 – Datei bereitstellen

1. Lade die Datei `index.html` herunter
2. Öffne sie **direkt im Browser** (Doppelklick) **oder** hoste sie lokal:

```bash
python3 -m http.server 8080
````

Dann im Browser öffnen:

```
http://localhost:8080
```

---

### 🔐 Schritt 2 – CORS in Moonraker aktivieren (WICHTIG)

Damit das Dashboard auf die Klipper-API zugreifen darf, **muss CORS erlaubt werden**.

Öffne deine `moonraker.conf` und ergänze (oder passe an):

```ini
[authorization]
cors_domains:
    https://my.mainsail.xyz
    http://my.mainsail.xyz
    http://*.local
    http://*.lan
    *

trusted_clients:
    10.0.0.0/8
    127.0.0.0/8
    169.254.0.0/16
    172.16.0.0/12
    192.168.0.0/16
    FE80::/10
    ::1/128
```

➡️ Danach **Moonraker neu starten**:

```bash
sudo service moonraker restart
```

---

### ➕ Schritt 3 – Drucker hinzufügen

1. Öffne das Dashboard
2. Klicke auf **„Drucker hinzufügen“**
3. Trage ein:

```
IP:PORT
z.B. 192.168.188.107:7125
```

4. Druckername optional vergeben (oben editierbar)

Die Daten werden automatisch im **LocalStorage** gespeichert.

---

### ⚠️ Sicherheitshinweis

Dieses Dashboard erlaubt **kritische Aktionen**:

* Print Cancel
* G-Code Senden
* Emergency Stop

➡️ **Nur im lokalen Netzwerk verwenden** oder über:

* VPN
* Reverse Proxy
* Zugriffsbeschränkung

ab
