# OpenFront.io - Lokales Singleplayer Setup

Diese Anleitung führt dich durch die Installation und den Betrieb von **OpenFront.io** als lokales Singleplayer-Spiel auf deinem Computer.

## 📋 Voraussetzungen

- **Node.js** v22+ (mit npm v11+)
- **Git** (zum Klonen des Repositories)
- Ein moderner Browser (Chrome, Firefox, Safari, Edge)
- ~2GB freier Speicher für Dependencies
- ~200MB freier Speicher für das Spiel

## 🚀 Installation

### Schritt 1: Repository klonen

```bash
cd c:\Users\Dennis\Desktop
git clone https://github.com/openfrontio/OpenFrontIO.git openfrontio-local
cd openfrontio-local
```

Das Repository ist bereits geklont unter:

```
c:\Users\Dennis\Desktop\openfrontio-original
```

### Schritt 2: Dependencies installieren

```bash
npm install
```

Dies installiert alle notwendigen Pakete (~1468 Pakete):

- **Frontend**: Webpack, Pixi.js, Lit, D3, Tailwind CSS
- **Backend**: Express, WebSocket, TypeScript
- **Development**: ESLint, Prettier, Jest, Husky

Die Installation dauert ca. 1-2 Minuten.

### Schritt 3: Umgebung konfigurieren

```bash
# Kopiere die Example-Env-Datei
cp example.env .env

# Optional: Bearbeite .env für spezifische Konfigurationen
```

Die `.env` Datei muss nicht bearbeitet werden für lokales Singleplayer-Spiel.

## 🎮 Spiel starten

### Option 1: Vollständiger Dev-Modus (empfohlen)

```bash
npm run dev
```

Dies startet:

- **Webpack Dev Server**: http://localhost:9000 (Frontend mit Hot Reload)
- **Master Server**: http://localhost:3000 (API Gateway)
- **Worker Process 0**: Port 3001 (Game Logic)
- **Worker Process 1**: Port 3002 (Game Logic)

### Option 2: Nur Frontend (Hot Reload)

```bash
npm run start:client
```

Das Frontend ist verfügbar auf: http://localhost:8080

### Option 3: Nur Backend

```bash
npm run start:server-dev
```

Der Server läuft auf: http://localhost:3000

## 🕹️ Gameplay

### Startbildschirm

Wenn du das Spiel öffnest, siehst du:

1. **Schwierigkeitswahl** - Wähle deine bevorzugte Schwierigkeit
2. **Kartenwahl** - Wähle eine der 30+ vordefinierten Karten
3. **Spieloptionen** - Konfiguriere Einstellungen (optional)

### Spielmechaniken

**Ziel**: Kontrolliere 72% des Territoriums zum Gewinnen

**Kontrollen**:

- **Linksklick**: Wähle ein Tile und starte Expansion
- **Rechtsklick**: Kontextmenü für Gebäudeoptionen
- **WASD / Pfeiltasten**: Navigiere auf der Karte
- **Mausrad**: Zoom
- **Leertaste**: Pause/Resume

**Gebäude bauen**:

1. Wähle ein leeres Tile in deinem Territorium
2. Klick auf "Build" → wähle Gebäudetyp
3. Kosten sind abhängig vom Gebäudetyp

**Gebäudetypen**:

- 🏛️ **City** - Verwaltungszentrum, +20 Ressourcen/Runde
- 🏭 **Factory** - Industrie, +40 Ressourcen/Runde
- ⚓ **Port** - Handel, +30 Ressourcen/Runde, benötigt Wasserzugang
- 🛡️ **Defense** - Schutz vor Expansion, Defensiv
- 📡 **General Quarter** - Spezialeinheit

**Ressourcen-Management**:

- Jedes Tile generiert Ressourcen
- Gebäude multiplizieren Ressourcen-Output
- Expansionieren kostet Ressourcen

**Militär-Einheiten**:

- **Infantry** - Standard Infanterie
- **Tank** - Gepanzert, stärker
- **Artillery** - Langstrecken-Angriff
- **Navy** - Seekrieg

### AI-Gegner (Singleplayer)

In Singleplayer spielst du gegen KI-Gegner:

- **Schwierigkeitsgrad beeinflusst KI-Verhalten**
- **Easy**: Passive Expansion, wenig Angriffe
- **Normal**: Ausgewogene Strategie
- **Hard**: Aggressive Expansion, koordinierte Angriffe
- **Insane**: Optimale Spielweise, schwer zu schlagen

## 🛠️ Development-Tipps

### Code bearbeiten und testen

Der **Hot Reload** funktioniert automatisch:

1. Bearbeite eine Datei in `src/client/` oder `src/server/`
2. Speichern → automatisches Reload
3. Browser aktualisiert sich selbst (Hot Module Replacement)

### Debug-Modus

Im Browser-Inspector (F12):

- **Console**: Fehler und Logs
- **Network**: API-Aufrufe beobachten
- **Performance**: FPS und Ladezeiten prüfen

### Testing

```bash
# Run Tests
npm test

# Test Coverage
npm test:coverage

# Lint Code
npm run lint

# Format Code
npm run format
```

## 📁 Projektstruktur

```
openfrontio-original/
├── src/
│   ├── client/           # Frontend (Pixi.js Canvas Rendering)
│   │   ├── ClientGameRunner.ts
│   │   ├── components/   # UI Components
│   │   ├── graphics/     # Sprite & Animation
│   │   └── styles/       # Tailwind CSS
│   │
│   ├── server/           # Backend (Express.js)
│   │   ├── Server.ts     # Main Server
│   │   ├── GameServer.ts # Game Logic
│   │   ├── Client.ts     # Client Management
│   │   └── Worker.ts     # Worker Processes
│   │
│   └── core/             # Shared Game Logic
│       ├── Tile.ts       # Tile-System
│       ├── Unit.ts       # Militär-Einheiten
│       ├── Building.ts   # Gebäude
│       └── Game.ts       # Game Rules
│
├── resources/            # Assets
│   ├── images/
│   ├── maps/             # Map Data
│   ├── sounds/
│   └── flags/            # Country Flags
│
├── webpack.config.js     # Build-Konfiguration
├── package.json          # Dependencies
└── .env                  # Environment Vars
```

## 🗺️ Karten

OpenFront.io enthält 30+ Karten:

- **Echtzeit-Landkarten** (Europa, Asien, Afrika, etc.)
- **Phantasie-Karten** (benutzerdefiniert)
- **Arena-Karten** (klein, schnell)

Die Karten sind in `resources/maps/` als `.json` Dateien definiert.

## ⚡ Performance

**Tipps für bessere Performance**:

1. Schließe andere Browser-Tabs
2. Reduziere Grafik-Qualität (Settings)
3. Nutze Hardware-Acceleration (Browser-Setting)
4. Verwende Chrome für beste Performance

**Performance-Monitoring**:

```bash
# Starte Performance-Test
npm run perf
```

## 🐛 Häufige Fehler

### "Port bereits in Benutzung"

```bash
# Windows: Finde und beende Prozess
netstat -ano | findstr :3000
taskkill /PID < PID > /F

# Oder nutze andere Ports über .env
```

### "Webpack Dev Server startet nicht"

```bash
# Versuche Port zurückzusetzen
rm -rf node_modules/.cache
npm run dev
```

### "WebSocket Verbindung fehlgeschlagen"

- Überprüfe dass Master Server auf Port 3000 läuft
- Überprüfe .env Konfiguration
- Versuche Browser-Cache zu löschen (Ctrl+Shift+Del)

### "Fehler beim Laden von Maps"

```bash
# Regeneriere Maps
npm run gen-maps
npm run format
npm run build-dev
```

## 📊 Architektur-Details

### Frontend Stack

**Pixi.js**: GPU-accelerated 2D Rendering

- Effiziente Sprite-Handling
- Große Map-Unterstützung
- Low-Latenz Rendering

**Lit**: UI Web Components

- Reactive State Management
- Kleine Bundle-Größe
- TypeScript Support

**Tailwind CSS**: Utility-First Styling

- Responsive Design
- Theme-System
- Hot Reload Support

### Backend Stack

**Node.js Cluster**: Mehrere Worker-Prozesse

- Load Balancing
- Fault Tolerance
- Master-Worker Kommunikation

**WebSocket**: Real-Time Kommunikation

- Bi-direktionale Kommunikation
- Low-Latency Gameplay
- Multiplayer-ready

**Express.js**: HTTP Server

- REST API
- Static File Serving
- Middleware System

### Gameplay Loop

```
1. Client: Spieler-Input (Klick, Taste)
2. Client: Input → Validation
3. Client: Prediction (optimistic update)
4. Client: Sende Command zu Server über WebSocket
5. Server: Validiere Command
6. Server: Führe Game Logic aus
7. Server: Update Game State
8. Server: Sende State-Update zu Clients
9. Client: Empfange Update
10. Client: Reconcile mit Prediction
11. Client: Render neuen State
12. → Zurück zu 1
```

## 🔒 Security Notes

- **OpenFront.io** verwendet **AGPL v3 Lizenz**
- Jede Modifikation/Fork muss Attribution enthalten
- Siehe [LICENSE](LICENSE) für komplette Terms

## 🤝 Contributing

Wenn du das Projekt verändern möchtest:

```bash
# Erstelle Feature-Branch
git checkout -b my-awesome-feature

# Mache Änderungen und teste
npm test
npm run lint:fix

# Committe
git add .
git commit -m "Add awesome feature"

# Push
git push origin my-awesome-feature
```

## 📚 Weitere Ressourcen

- **GitHub**: https://github.com/openfrontio/OpenFrontIO
- **Wiki**: https://openfront.miraheze.org/wiki/OpenFront.io
- **Discord**: https://discord.gg/K9zernJB5z
- **Crowdin (Übersetzungen)**: https://crowdin.com/project/openfront-mls

## 🎓 Lernen vom Code

**Interessante Dateien zum Studieren**:

- `src/core/Game.ts` - Komplette Spiellogik
- `src/client/ClientGameRunner.ts` - Rendering Loop
- `src/server/GameServer.ts` - Server-Side Logic
- `src/core/Tile.ts` - Tile-System
- `src/core/Unit.ts` - Militär-Mechaniken

Dies sind exzellente Referenzen zum Lernen über:

- Game Development in TypeScript
- Multiplayer Synchronisierung
- Canvas Rendering (Pixi.js)
- Real-Time Game Servers

## 💡 Tipps für Singleplayer

1. **Früh expandieren**: Beanspruche Land schnell am Anfang
2. **Gebäude planen**: Platziere Fabriken neben Ressourcen-Rich Areas
3. **Militär aufbauen**: Bereit sein für KI-Angriffe
4. **Ressourcen-Management**: Nicht zu viel auf Militär ausgeben
5. **Schwierigkeitsgrad anpassen**: Start mit Easy/Normal

## 🚀 Nächste Schritte

1. Spiele mehrere Runden um Mechaniken zu lernen
2. Experimentiere mit verschiedenen Strategien
3. Teste mit unterschiedlichen Maps und Schwierigkeitsgraden
4. Schau dir den Code an - viel zu lernen!
5. Modifiziere Game-Regeln oder Add Features

---

**Viel Spaß mit OpenFront.io! 🎮**

Das Spiel ist lokal installiert und läuft auf deinem Computer. Öffne einfach http://localhost:9000 im Browser und starte zu spielen!
