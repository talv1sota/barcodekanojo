# Barcode Kanojo

An iOS revival of Cybird's Barcode Kanojo -- a mobile game where scanning real-world barcodes generates unique anime girlfriends (kanojos) with distinct personalities and stats.

## Overview

This project is a full reimplementation of the original Barcode Kanojo experience:

- **Scan barcodes** to generate or discover kanojos tied to real products
- **Interact** with your kanojo via Live2D touch, dates, and gifts
- **Build relationships** -- raise love gauges, manage stamina, earn rewards
- **Social features** -- visit other players' kanojos, like them, check rankings
- **Live2D avatars** -- fully animated characters with customizable parts (hair, eyes, clothes, accessories)

## Project Structure

```
barcodekanojo/
  BarcodeKanojo-iOS/     # SwiftUI iOS client
  barcode-kanojo-server/  # Python/FastAPI backend
  live2d-v2/              # Live2D rendering engine (Swift/Metal)
```

### iOS Client

Built with **SwiftUI** targeting iOS 16+. Uses MVVM architecture.

Key features:
- Barcode scanning via AVFoundation
- Live2D avatar rendering with Metal
- Date/gift system with item menus
- Stamina and money management
- Tutorial overlay for new players
- Push notification support
- Enemy book and map views

### Server

**Python/FastAPI** backend with SQLite database.

- RESTful API matching the original Cybird endpoints
- User authentication with SHA-512 password hashing
- Kanojo generation from barcode data
- Date, gift, and social interaction endpoints
- Avatar data serving for Live2D models

### Live2D Engine

A **Swift/Metal** port of the Live2D v2 SDK for rendering animated kanojo avatars. Supports:
- MOC file parsing and model rendering
- Part-based avatar customization
- Touch interaction with body regions
- Idle and reaction animations
- Device motion-based parallax

## Setup

### Server

```bash
cd barcode-kanojo-server
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env  # edit as needed
python main.py
```

The server runs on `http://localhost:8000` by default.

### iOS

1. Open `BarcodeKanojo-iOS/BarcodeKanojo.xcodeproj` in Xcode
2. Build and run on a simulator or device (iOS 16+)
3. On first launch, configure the server URL in Settings to point to your server

## Credits

Based on the original **Barcode Kanojo** by Cybird. Android reference implementation by [Goujer](https://github.com/nicl83/kanojo_app).

## License

This project is for educational and preservation purposes.
