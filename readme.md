# 🌀 Dancing Lights

Interaktives 360°-Visuals-Projekt mit TouchDesigner, Orbbec-Kamera und Smartphone-Sensoren. Entwickelt im Rahmen des Minor Creative Technology.

![GIF Preview](/media/TD_CamCube.gif)

---

## 🎬 Projektübersicht

> **Video-Demo ansehen:**  
> [![YouTube Video](https://img.youtube.com/vi/KIz1tBnaqec/1.jpg)](https://youtu.be/KIz1tBnaqec)

Ziel war es, eine immersive Projektion im Igloo-Raum zu entwickeln, bei der sich visuelle Elemente reaktiv zur Musik und den Bewegungen des Nutzers verändern.  
Highlights:

- Echtzeit-Partikelsysteme, gesteuert über Handtracking
- Farbveränderung durch Smartphone-Sensoren (ZIG Sim)
- Audioreaktive 3D-Cubes mit Licht- und Glow-Effekten

---

## 🧩 Komponentenplan

### Digitale Medienkomponenten
- **TouchDesigner**: Zentrale Software für Visualisierung und Interaktion
- **Orbbec Astra Kamera**: Handtracking zur Steuerung der Partikelbewegung
- **ZIG Sim App**: Smartphone-Sensorwerte per Netzwerk an TouchDesigner übertragen
- **Musikinput**: Beliebiger Song für Audioanalyse (z. B. Kick-Erkennung)

### Kommunikationswege
| Quelle           | Ziel             | Protokoll   |
|------------------|------------------|-------------|
| Smartphone (ZIG Sim) | TouchDesigner   | Netzwerk / OSC |
| Orbbec Kamera    | TouchDesigner   | USB / SDK   |
| Musik            | TouchDesigner   | Internal Audio Analyse |

---

## ⚙️ Reproduzierbarkeit: Projekt einrichten

### Voraussetzungen
- TouchDesigner (aktuelle Version)
- Orbbec Astra Treiber + SDK
- ZIG Sim App auf Smartphone installiert
- Netzwerkverbindung zwischen Smartphone & PC

### Schritt-für-Schritt Anleitung

1. Projektdatei in TouchDesigner öffnen (`IglooDance_Orbbec - halfRes.toe`)
2. Orbbec-Kamera verbinden und sicherstellen, dass das Handtracking aktiviert ist
3. ZIG Sim starten und relevante Sensorwerte (Accelerometer, Quaternion) aktivieren
4. Musik-Input hinzufügen (Audiofile, solange es den Kick registriert)
5. Über 'TOPsyphonspoutout' projizieren

---

## ✨ Interaktive Module

### 🌪️ Particle Vortex

- Generiert mit `SOPparticle` und `SOPsphere`
- Steuerung über Handposition (Orbbec)
- Partikel kreisen um `SOPmetaball` via `SOPforce`
- Farbsteuerung über `TOPramp`, beeinflusst durch ZIG Sim-Werte

**Screenshot: Handtracking der Partikel**
![Handtracking Partikel](/media/TD_Orbbec_Handtracking.png)

**Screenshot: Farbsteuerung via ZIG Sim**
![Farbsteuerung ZIG Sim](/media/TD_ZigSim.png)

---

### 🔊 Audioreaktive Cubes

- Zwei Cubes: innerer (gelb), äusserer (blau)
- Rotation und Grösse reagieren auf Audio-Kick
- Visual Effects: `Glow`, `LightTunnel`
- Audioparameter werden analysiert und auf `geo1` & `geo2` gemappt

**Screenshot: 3D-Cube Reaktion auf Musik**
![3D Cube Kick](/media/TD_3DCube_MusicKick.png)

---

## 🖥️ Projektion Setup

- Visualisierung wurde für eine Igloo-Kuppel mit 360°-Beamerprojektion entwickelt
- Das Projekt musste auf sehr hohe Auflösung angepasst werden. Als Trick wurde nur die halbe Auflösung verwendet und dann im Output (ausserhalb des TD Programms) verdoppelt.
- Herausforderungen bei Lichtverhältnissen und Kalibrierung

**Screenshot: Projektionssetup im Igloo**
![Projektion Setup](/media/TD_ProjektionSetup.png)

---

## ⚠️ Bekannte Probleme

| Problem | Beschreibung |
|--------|--------------|
| **Cube-Rendering** | Vertikale Trennungen, kein immersiver Effekt |
| **Vortex-Logik** | Partikel verhalten sich inkonsistent im Igloo-Setup |
| **Handtracking (Orbbec)** | Ungenaue Handposition, hohe Latenz, falsche Bewegungswerte |

---

## 🧪 Entwicklungsprozess & Erkenntnisse

### Herausforderungen
- CPU-Auslastung durch Partikelmenge → Optimierung notwendig
- Orbbec-Tracking unzuverlässig bei schwachem Licht & schnellen Bewegungen
- Unterschiedliche Anforderungen zwischen MediaPipe-Prototyp & Igloo-Setup

### Verworfen
- Alternative Handtracking-Systeme (z. B. MediaPipe)
- Komplexe Partikelrotation um spezifische Finger

### Erkenntnisse
- Umfangreiche Erfahrung mit TouchDesigner-Nodes und Strukturen
- Tieferes Verständnis für Systemperformance & Echtzeitdaten
- Umgang mit technischen Limitierungen und Umplanung

### Hilfsmittel
- YouTube-Tutorials (z. B. Particle-Systeme, Audio-Reactive-Design)
- Eigene Tests in verschiedenen Auflösungen (Home Setup vs. Igloo)

---

## 🎯 Fazit

Die ursprüngliche Vision – durch Tanzbewegungen im Igloo verschiedene Effekte auszulösen – konnte technisch nicht vollständig umgesetzt werden.  
Grund: Limitationen des Trackings (Orbbec), hohe Latenz, sowie Lichtverhältnisse im Igloo. Dennoch entstand ein interaktives Erlebnis mit spannenden Partikel- und Audioeffekten.

> **Wunsch für die Zukunft:**  
> Einfacheres Setup mit präzisem Tracking, besserer Lichtsteuerung und intuitiver Bedienbarkeit vor Ort.

---

## 📎 Anhang

- Projektdatei: `IglooDance_Orbbec - halfRes.toe`
- Screenshots / Videos: im Ordner `/media`