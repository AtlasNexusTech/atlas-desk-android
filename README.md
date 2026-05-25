# Atlas Desk — Android Client

P2P remote desktop Android app. Connects to any Atlas Desk agent (Go binary) via WebRTC.

## How it works

1. **Run the agent** on the remote PC: `./atlas-desk-agent -signal ws://YOUR_SERVER:8800/ws`
2. **Run the signaling server**: `./atlas-desk-signaling`
3. **Open the Android app**, enter the agent's ID or alias (e.g. `PC Bureau`), tap Connect
4. Control the remote PC — mouse, keyboard, clipboard, file transfer

## Build

```bash
npm install
npx cap sync android
cd android && ./gradlew assembleDebug
```

APK output: `android/app/build/outputs/apk/debug/app-debug.apk`

## CI

GitHub Actions builds the APK on every push to `main`. Download the artifact from Actions tab.

## Architecture

- **Client**: Capacitor Android wrapper around the Atlas Desk web client (`www/index.html`)
- **WebRTC**: P2P connection via pion/webrtc — no server relays data after initial handshake
- **Signaling**: Go WebSocket server (separate repo: `AtlasNexusTech/atlas-desk/signaling/`)
- **Agent**: Go binary running on the remote PC (`AtlasNexusTech/atlas-desk/agent/`)

## Config

The app serves the client locally from the APK bundle. On first launch, configure:
- **Signal Server URL** → URL of your Atlas Desk signaling server (e.g. `ws://192.168.1.100:8800/ws`)
- **Agent ID or Alias** → The remote PC's ID (9-digit number) or alias (e.g. `PC Bureau`)

## License

MIT — part of the Atlas Desk project.
