# EVON Obfuscator - Update Server

This repository hosts the update manifest for EVON Obfuscator's auto-update system.

## How It Works

1. When users open EVON, it fetches `update-manifest.json` from this repo
2. The app compares the version in the manifest with the installed version
3. If a newer version exists, users are prompted to update

## Files

- `update-manifest.json` - The main file the app checks (KEEP THIS UPDATED!)
- `EXAMPLE-*.json` - Examples for reference (don't upload these)

## How to Release an Update

### Step 1: Build Your New Version
Build the new `.exe` installer with Tauri

### Step 2: Create a GitHub Release
1. Go to **Releases** → **Create new release**
2. Tag: `v1.1.0` (match your version number)
3. Upload `EVON-Setup.exe`
4. Publish the release

### Step 3: Update the Manifest
Edit `update-manifest.json`:

```json
{
  "version": "1.1.0",           // ← New version number
  "releaseDate": "2025-03-01",  // ← Today's date
  "isCritical": false,          // ← true for security updates
  "changelog": [
    { "type": "feature", "text": "What you added" },
    { "type": "fix", "text": "What you fixed" },
    { "type": "security", "text": "Security patches" },
    { "type": "improvement", "text": "What you improved" }
  ],
  "downloadUrl": "https://github.com/YOUR_USERNAME/evon-releases/releases/download/v1.1.0/EVON-Setup.exe"
}
```

### Step 4: Commit & Push
```bash
git add update-manifest.json
git commit -m "Release v1.1.0"
git push
```

That's it! Users will be prompted to update next time they open EVON.

## Changelog Types

| Type | Icon | When to Use |
|------|------|-------------|
| `security` | 🛡️ | Security fixes, vulnerability patches |
| `feature` | ✨ | New features |
| `fix` | 🐛 | Bug fixes |
| `improvement` | ⚡ | Performance, UX improvements |

## Critical Updates

Set `"isCritical": true` for security updates. This:
- Shows a red warning banner
- Ignores "Skip This Version" preference
- Strongly encourages users to update
