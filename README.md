# JMAD Installer - Official Curated List

**Version**: 1.1.0
**Last Updated**: November 8, 2025
**Total Apps**: 22

Official curated application list for the [JMAD Installer](https://github.com/YOUR-USERNAME/JMAD-Installer).

---

## About

This repository hosts the official curated list of applications available in JMAD Installer. The installer can fetch this list automatically to provide users with pre-configured, tested applications ready for silent installation.

**Features**:
- ✅ 22 pre-configured applications
- ✅ Silent install arguments tested and verified
- ✅ GitHub Releases API integration for auto-updating apps
- ✅ Offline and online installation modes
- ✅ Categorized by usage (gaming, development, utilities, etc.)

---

## Usage

### For JMAD Installer

The installer fetches this list from:
```
https://raw.githubusercontent.com/YOUR-USERNAME/JMAD-Curated-List/main/curated-list.json
```

Configure in JMAD Installer:
1. Open Settings tab
2. Add curated source URL
3. Click "Refresh Curated Lists"

### Direct Download

```bash
curl -O https://raw.githubusercontent.com/YOUR-USERNAME/JMAD-Curated-List/main/curated-list.json
```

Or download manually:
[curated-list.json](https://raw.githubusercontent.com/YOUR-USERNAME/JMAD-Curated-List/main/curated-list.json)

---

## File Format

```json
{
  "last_updated": "2025-11-08T00:00:00Z",
  "source": "official",
  "version": "1.1.0",
  "applications": [
    {
      "id": "unique-app-id",
      "name": "Application Name",
      "type": "offline|online",
      "download_url": "https://...",
      "version": "latest|x.y.z",
      "silent_args": ["/S"],
      "fallback_args": ["/VERYSILENT"],
      "github_owner": "owner-name",
      "github_repo": "repo-name",
      "github_asset_pattern": "installer.exe",
      "notes": "Description"
    }
  ]
}
```

### Fields

- **`id`** (string, required): Unique identifier (kebab-case)
- **`name`** (string, required): Display name
- **`type`** (string, required): `"offline"` (bundled) or `"online"` (downloaded at install)
- **`download_url`** (string, nullable): Direct download URL (null if using GitHub API)
- **`version`** (string, optional): Version number or "latest"
- **`silent_args`** (array, required): Primary silent install arguments
- **`fallback_args`** (array, optional): Fallback arguments if primary fails
- **`github_owner`** (string, optional): GitHub repository owner for dynamic resolution
- **`github_repo`** (string, optional): GitHub repository name
- **`github_asset_pattern`** (string, optional): Pattern to match release asset filename
- **`notes`** (string, optional): Description or notes

---

## Applications (22 total)

### Gaming (5 apps)
- **Steam** - Gaming platform
- **Epic Games Launcher** - Epic Games Store
- **EA Desktop** - EA Games launcher
- **Discord** - Voice and text chat (Stable)
- **Discord PTB** - Discord Public Test Build

### Development (4 apps)
- **Visual Studio Code** - Code editor
- **GitHub Desktop** - GitHub client
- **Microsoft PowerToys** - Windows utilities (GitHub dynamic)
- **UltiMaker Cura** - 3D printing slicer (GitHub dynamic)

### Browsers (2 apps)
- **Google Chrome** - Web browser
- **Mozilla Firefox** - Web browser

### Utilities (7 apps)
- **7-Zip** - File archiver (GitHub dynamic, offline curated)
- **Notepad++** - Text editor (GitHub dynamic, offline curated)
- **Free Download Manager** - Download manager
- **Process Lasso** - Process optimization
- **CPU-Z** - CPU information utility
- **MobaXterm** - SSH/X11 terminal
- **OBS Studio** - Streaming and recording

### Communication (2 apps)
- **TeamSpeak 3** - Voice chat client
- *(Discord also listed in Gaming)*

### VR (1 app)
- **Virtual Desktop Streamer** - VR desktop streaming

### Drivers (1 app)
- **NVIDIA App** - NVIDIA driver and control panel

### Simulation (1 app)
- **DCS World** - Digital Combat Simulator

---

## GitHub Dynamic Resolution

The following apps use GitHub Releases API to automatically fetch the latest version:

### Offline Curated Apps (Download at Build-Time)
- **Notepad++** (`notepad-plus-plus/notepad-plus-plus`)
- **7-Zip** (`ip7z/7zip`)

### Online Dynamic Apps (Download at Install-Time)
- **Microsoft PowerToys** (`microsoft/PowerToys`)
- **UltiMaker Cura** (`Ultimaker/Cura`)

These apps do NOT require manual version updates. The installer queries GitHub's API for the latest release automatically.

---

## Maintenance

### Updating Apps with Direct URLs

For apps with `download_url`:
1. Check vendor website for latest download link
2. Update `download_url` field
3. Update `version` field if applicable
4. Test download link
5. Commit and push

### GitHub Dynamic Apps

No maintenance needed - these apps fetch the latest release automatically via GitHub Releases API.

### Adding New Apps

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding new applications.

---

## Pending Apps

The following apps are being considered for addition but require additional work:

- **Ubisoft Connect** - Requires direct download link
- **Visual Studio Community** - Requires direct download link
- **Bulk Rename Utility** - Requires direct download link
- **Java** - Requires license acceptance mechanism
- **Pyenv** - GitHub archive, may need extraction script

---

## Version History

### v1.1.0 (November 8, 2025)
- ✅ Added GitHub Releases API integration
- ✅ Added Notepad++ as offline curated app (GitHub dynamic)
- ✅ Added 7-Zip as offline curated app (GitHub dynamic)
- ✅ Updated PowerToys with GitHub metadata
- ✅ Updated UltiMaker Cura with GitHub metadata
- ✅ 4 apps now use dynamic GitHub resolution

### v1.0.0 (November 7, 2025)
- ✅ Initial release with 18 applications
- ✅ All apps tested and verified
- ✅ Silent install arguments configured

---

## Testing

All applications have been tested for:
- ✅ Download link validity
- ✅ Silent installation success
- ✅ Fallback arguments (where applicable)

Test environment:
- Windows 10/11 x64
- Clean virtual machines
- Standard user + admin elevation

---

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for:
- How to submit new applications
- Testing requirements
- Pull request guidelines
- Code of conduct

---

## License

This curated list is released under the **MIT License**.

The applications listed are property of their respective owners and are subject to their own licenses.

---

## Support

**Issues**: [GitHub Issues](https://github.com/YOUR-USERNAME/JMAD-Curated-List/issues)
**Main Project**: [JMAD Installer](https://github.com/YOUR-USERNAME/JMAD-Installer)

---

## JSON Schema

For validation, see the JSON schema at: [schema.json](schema.json)

---

**Maintained by**: JMAD Gaming
**Repository**: https://github.com/YOUR-USERNAME/JMAD-Curated-List
**License**: MIT
