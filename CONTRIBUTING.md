# Contributing to JMAD Curated List

Thank you for your interest in contributing to the JMAD Installer curated list!

---

## How to Contribute

### Adding a New Application

1. **Fork this repository**
2. **Create a new branch**: `git checkout -b add-app-name`
3. **Add your application** to `curated-list.json`
4. **Test the application** (see Testing Requirements below)
5. **Submit a pull request**

---

## Application Requirements

### Must Have
- ✅ **Windows installer** (.exe, .msi)
- ✅ **Silent install capability** (no user interaction required)
- ✅ **Free or publicly available** (freemium acceptable, but installer must be free)
- ✅ **Direct download link** or **GitHub Releases API compatible**
- ✅ **Tested on Windows 10/11 x64**

### Should Have
- ✅ Stable release (not beta or nightly unless explicitly marked)
- ✅ Popular/widely-used application
- ✅ Actively maintained
- ✅ Legitimate source (official vendor website or verified mirror)

### Nice to Have
- ✅ GitHub Releases for automatic version updates
- ✅ Fallback install arguments for compatibility
- ✅ Uninstall command or script

---

## Testing Requirements

Before submitting, you must test your application:

### 1. Download Test
```bash
# Verify download link is accessible
curl -I <download_url>
# Should return 200 OK or 302 redirect
```

### 2. Silent Install Test

**Primary silent args**:
```cmd
installer.exe /S
# OR
msiexec /i installer.msi /quiet /norestart
```

**Verify**:
- ✅ No UI appears
- ✅ Application installs successfully
- ✅ No errors or prompts
- ✅ Application appears in Programs & Features

**If primary fails**, test **fallback args**:
```cmd
installer.exe /VERYSILENT
```

### 3. Cleanup Test
```cmd
# Verify application can be uninstalled
# Check Programs & Features or use uninstall command
```

---

## Application Template

### Standard Application (Direct URL)

```json
{
  "id": "app-name-online",
  "name": "Application Name",
  "type": "online",
  "download_url": "https://example.com/installer.exe",
  "version": "x.y.z",
  "silent_args": ["/S"],
  "fallback_args": ["/VERYSILENT"],
  "launch_argument_template_id": "nsis-standard",
  "script": null,
  "uninstall_script": null,
  "uninstall_command": null,
  "checksum": null,
  "notes": "Description - Installer type",
  "include_in_build": false,
  "allow_manual_install": true
}
```

### GitHub Dynamic Application (Offline Curated)

```json
{
  "id": "app-name-offline-curated",
  "name": "Application Name",
  "type": "offline",
  "download_url": null,
  "version": "latest",
  "silent_args": ["/S"],
  "fallback_args": ["/VERYSILENT"],
  "launch_argument_template_id": "nsis-standard",
  "script": null,
  "uninstall_script": null,
  "uninstall_command": null,
  "checksum": null,
  "notes": "Description - Offline curated (downloads from GitHub to local)",
  "include_in_build": false,
  "allow_manual_install": true,
  "github_owner": "owner-name",
  "github_repo": "repo-name",
  "github_asset_pattern": "installer-x64.exe"
}
```

### GitHub Dynamic Application (Online)

```json
{
  "id": "app-name-online",
  "name": "Application Name",
  "type": "online",
  "download_url": null,
  "version": "latest",
  "silent_args": ["/S"],
  "fallback_args": ["/VERYSILENT"],
  "launch_argument_template_id": "nsis-standard",
  "script": null,
  "uninstall_script": null,
  "uninstall_command": null,
  "checksum": null,
  "notes": "Description - Dynamically fetches latest from GitHub",
  "include_in_build": false,
  "allow_manual_install": true,
  "github_owner": "owner-name",
  "github_repo": "repo-name",
  "github_asset_pattern": "installer-x64.exe"
}
```

---

## Field Guidelines

### `id`
- **Format**: lowercase-kebab-case
- **Suffix**: `-online` or `-offline-curated`
- **Unique**: Must not conflict with existing IDs
- **Example**: `notepadplusplus-offline-curated`

### `name`
- **Format**: Proper capitalization, official branding
- **Example**: `Notepad++` (not `notepad++` or `NotepadPlusPlus`)

### `type`
- **`offline`**: Bundled in installer (downloaded at build time)
- **`online`**: Downloaded during installation (requires internet)

### `download_url`
- **Direct link** to installer file
- **Must be HTTPS** (unless verified mirror)
- **Stable URL** preferred (avoid version-specific paths if possible)
- **Use `null`** if using GitHub Releases API

### `version`
- **Specific version**: `"8.8.7"`
- **Latest**: `"latest"` (for GitHub dynamic or auto-updating installers)
- **Update regularly** for version-pinned apps

### `silent_args`
- **Array of strings**: `["/S"]` not `"/S"`
- **Tested and verified**: Must result in silent install
- **Common patterns**:
  - NSIS: `["/S"]`
  - InnoSetup: `["/VERYSILENT", "/NORESTART"]`
  - MSI: `["/quiet", "/norestart"]`

### `fallback_args`
- **Alternative silent arguments** if primary fails
- **Optional** but recommended

### `github_owner`, `github_repo`, `github_asset_pattern`
- **Use for GitHub-hosted apps** with Releases
- **`github_asset_pattern`**: Substring to match asset filename
  - Example: `"installer.x64.exe"` matches `npp.8.8.7.Installer.x64.exe`
- **Test resolution**: Verify correct asset is matched

### `notes`
- **Brief description** (1-2 sentences)
- **Installer type** (e.g., "NSIS installer", "MSI package")
- **Special notes** (e.g., "Requires admin", "ZIP archive contains installer")

---

## Common Installer Types

### NSIS (Nullsoft Scriptable Install System)
```json
{
  "silent_args": ["/S"],
  "fallback_args": ["/silent"],
  "launch_argument_template_id": "nsis-standard"
}
```

### InnoSetup
```json
{
  "silent_args": ["/VERYSILENT", "/NORESTART"],
  "fallback_args": ["/SILENT"],
  "launch_argument_template_id": "innosetup-standard"
}
```

### MSI (Windows Installer)
```json
{
  "silent_args": ["/quiet", "/norestart"],
  "fallback_args": ["/qn"],
  "launch_argument_template_id": "msi-standard"
}
```

### Generic/Custom
```json
{
  "silent_args": ["-silent", "-install"],
  "fallback_args": ["/S"],
  "launch_argument_template_id": "generic-silent"
}
```

---

## Pull Request Checklist

Before submitting your PR:

- [ ] Application tested on Windows 10/11 x64
- [ ] Silent install works without user interaction
- [ ] Download URL is valid and accessible
- [ ] JSON is valid (no syntax errors)
- [ ] `id` is unique and follows naming convention
- [ ] All required fields are filled
- [ ] Notes include installer type
- [ ] Application is free or publicly available
- [ ] PR description explains why app should be added

---

## Review Process

1. **Automated checks**: JSON validation, URL accessibility
2. **Manual testing**: Maintainer will test silent install
3. **Approval**: Merged if all checks pass
4. **Rejection**: If tests fail, maintainer will provide feedback

**Expected turnaround**: 2-7 days

---

## Updating Existing Apps

### Version Updates

If a versioned app has a new release:

1. Update `download_url` with new version URL
2. Update `version` field
3. Test new installer
4. Submit PR with version update

### GitHub Dynamic Apps

**No action needed** - these apps fetch the latest release automatically.

### Broken Links

If you discover a broken download link:

1. Find the new official download link
2. Update `download_url`
3. Test new link
4. Submit PR with fix

---

## Questions?

- **Issues**: [GitHub Issues](https://github.com/YOUR-USERNAME/JMAD-Curated-List/issues)
- **Discussions**: [GitHub Discussions](https://github.com/YOUR-USERNAME/JMAD-Curated-List/discussions)
- **Main Project**: [JMAD Installer](https://github.com/YOUR-USERNAME/JMAD-Installer)

---

Thank you for contributing! 🎉
