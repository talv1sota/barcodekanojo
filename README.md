<p align="center">
  <h1 align="center">Barcode Kanojo</h1>
  <p align="center">
    <em>An iOS revival of Cybird's Barcode Kanojo</em>
  </p>
  <p align="center">
    <img src="https://img.shields.io/badge/platform-iOS_16%2B-blue?logo=apple" alt="Platform">
    <img src="https://img.shields.io/badge/swift-5.9-orange?logo=swift" alt="Swift">
    <img src="https://img.shields.io/badge/backend-FastAPI-009688?logo=fastapi" alt="Backend">
    <img src="https://img.shields.io/badge/rendering-Live2D_v2-ff69b4" alt="Live2D">
    <img src="https://img.shields.io/badge/license-Educational-lightgrey" alt="License">
    <img src="https://img.shields.io/badge/status-Work_in_Progress-yellow" alt="Status">
  </p>
</p>

---

> **[Work in Progress]** — Scan real-world barcodes to generate unique kanojos with distinct personalities, stats, and fully animated Live2D avatars.

---

## Features

| Feature | Description |
|---------|-------------|
| **Barcode Scanning** | Scan any product barcode to generate or discover a kanojo |
| **Live2D Avatars** | Fully animated characters with customizable hair, eyes, clothes, accessories |
| **Touch Interaction** | Tap, double-tap, and shake to interact -- each body region triggers unique reactions |
| **Dating System** | Take your kanojo on dates with timed animations and stamina costs |
| **Gift System** | Browse store/owned items, give gifts to raise love |
| **Love Gauge** | Build your relationship over time through interactions |
| **Stamina & Money** | Resource management -- actions cost stamina and money |
| **Social** | Visit other players' kanojos, like them, check rankings |
| **Enemy Book** | Track rival players who've interacted with your kanojos |
| **Map View** | Discover nearby kanojos on an interactive map |
| **Tutorial** | Guided onboarding for new players |
| **Push Notifications** | Stay updated on kanojo events |

---

## Project Structure

```
barcodekanojo/
├── BarcodeKanojo-iOS/          # SwiftUI iOS client
│   └── BarcodeKanojo/
│       ├── App/                # App entry point, delegate
│       ├── Configuration/      # Constants, settings
│       ├── Enums/              # ActivityType, RelationStatus, etc.
│       ├── Live2D/             # Live2D v2 engine (Swift/Metal)
│       │   ├── Core/           # Model parsing, rendering, deformers
│       │   └── Kanojo/         # Avatar model, animations, touch
│       ├── Models/             # Data models (Kanojo, User, Item, etc.)
│       ├── Networking/         # API client, image cache
│       ├── Security/           # Password hashing
│       ├── ViewModels/         # MVVM view models
│       └── Views/              # SwiftUI views
│           ├── Auth/           # Login, signup, server config
│           ├── Common/         # Shared components (gauges, charts)
│           ├── Dashboard/      # Activity timeline
│           ├── EnemyBook/      # Rival tracking
│           ├── Kanojos/        # Room, info, date/gift menus
│           ├── Map/            # Nearby kanojo map
│           ├── Scan/           # Barcode scanner
│           └── Settings/       # Profile, ticket shop, notifications
│
├── barcode-kanojo-server/      # Python/FastAPI backend
│   ├── api/                    # Route handlers
│   ├── models/                 # SQLAlchemy models
│   ├── schemas/                # Pydantic schemas
│   ├── migrations/             # Database migrations
│   └── config.py               # Server configuration
│
└── live2d-v2/                  # Live2D rendering engine (submodule)
```

---

## Tech Stack

### iOS Client

| Component | Technology |
|-----------|-----------|
| **UI Framework** | SwiftUI |
| **Architecture** | MVVM with `@StateObject` / `@Published` |
| **Min Target** | iOS 16.0 |
| **Barcode Scanning** | AVFoundation |
| **Avatar Rendering** | Custom Live2D v2 engine (Metal) |
| **Networking** | async/await + URLSession |
| **Image Caching** | Custom `ImageCache` with NSCache |
| **Persistence** | `@AppStorage` / UserDefaults |
| **Notifications** | UNUserNotificationCenter |

### Server

| Component | Technology |
|-----------|-----------|
| **Framework** | FastAPI (Python) |
| **Database** | SQLite via SQLAlchemy (async) |
| **Auth** | SHA-512 password hashing |
| **API Style** | REST (matching original Cybird endpoints) |
| **Config** | Pydantic Settings + `.env` |

### Live2D Engine

| Component | Technology |
|-----------|-----------|
| **Rendering** | Metal (GPU-accelerated) |
| **Model Format** | MOC (Live2D v2) |
| **Features** | Part-based customization, touch regions, idle/reaction animations, device motion parallax |

---

## Getting Started

### Prerequisites

- **Xcode 15+** (with iOS 16 SDK)
- **Python 3.10+**
- **macOS** (for iOS development)

### 1. Clone the repo

```bash
git clone https://github.com/talv1sota/barcodekanojo.git
cd barcodekanojo
```

### 2. Set up the server

```bash
cd barcode-kanojo-server
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Create your environment config:

```bash
cp .env.example .env
```

> **Note:** Edit `.env` to set a unique `SECRET_KEY` for production use.

Start the server:

```bash
python main.py
```

The server runs on `http://localhost:8000` by default.

### 3. Build the iOS app

1. Open `BarcodeKanojo-iOS/BarcodeKanojo.xcodeproj` in Xcode
2. Select your target device or simulator (iOS 16+)
3. **Build & Run** (`Cmd + R`)
4. On first launch, go to **Settings** and configure the server URL

---

## Architecture

```
┌──────────────┐     HTTP/JSON     ┌──────────────────┐
│              │  ◄──────────────► │                  │
│   iOS App    │                   │  FastAPI Server   │
│  (SwiftUI)   │                   │   (Python)        │
│              │                   │                  │
│  ┌────────┐  │                   │  ┌────────────┐  │
│  │Live2D  │  │                   │  │  SQLite DB  │  │
│  │Engine  │  │                   │  └────────────┘  │
│  │(Metal) │  │                   │                  │
│  └────────┘  │                   │  ┌────────────┐  │
│              │                   │  │ Avatar Data │  │
│  ┌────────┐  │                   │  └────────────┘  │
│  │ MVVM   │  │                   │                  │
│  │ViewModels│ │                   │  ┌────────────┐  │
│  └────────┘  │                   │  │   Static    │  │
│              │                   │  │   Assets    │  │
└──────────────┘                   │  └────────────┘  │
                                   └──────────────────┘
```

---

## Game Mechanics

### Relationships

| Status | Description |
|--------|-------------|
| **Kanojo** | Your own kanojo -- full interaction available |
| **Friend** | A friend's kanojo -- can gift and like |
| **Other** | Another player's kanojo -- can gift and like |

### Resources

| Resource | Usage |
|----------|-------|
| **Stamina** | Consumed by actions: dates (10), gifts (5), touch (1) |
| **Money (¥)** | Spent on date spots and gift items |
| **Tickets** | Premium currency for the ticket shop |
| **Love Gauge** | Relationship meter -- raised through interactions |

### Interactions

| Action | Cost | Effect |
|--------|------|--------|
| **Touch** | 1 stamina | +1 love, triggers animation |
| **Date** | 10 stamina + item price | Large love boost, timed state |
| **Gift** | 5 stamina + item price | Medium love boost, dialogue |
| **Like** | Free | Toggle heart on any kanojo |

---

## Credits

Based on the original **Barcode Kanojo** by [Cybird](https://www.cybird.co.jp/). Android reference implementation by Goujer.

---

## License

This project is for **educational and preservation purposes**. All original Barcode Kanojo assets and trademarks belong to their respective owners.
