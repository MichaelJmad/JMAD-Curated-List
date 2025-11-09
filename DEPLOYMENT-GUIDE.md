# JMAD Curated List - Deployment Guide

This guide explains how to publish the curated list repository to GitHub and configure JMAD Installer to use it.

---

## Prerequisites

- GitHub account
- Git installed and configured
- JMAD Curated List repository (already created locally)

---

## Step 1: Create GitHub Repository

### Option A: Via GitHub Web Interface (Recommended)

1. Go to https://github.com/new
2. Configure repository:
   - **Repository name**: `JMAD-Curated-List`
   - **Description**: `Official curated application list for JMAD Installer`
   - **Visibility**: ✅ **Public** (important!)
   - **Initialize repository**: ❌ Leave unchecked (we already have files)
3. Click **Create repository**

### Option B: Via GitHub CLI (if installed)

```bash
# Install GitHub CLI first: https://cli.github.com/
gh repo create JMAD-Curated-List --public --description "Official curated application list for JMAD Installer"
```

---

## Step 2: Push to GitHub

After creating the repository, GitHub will show commands. Use these:

```bash
cd L:\Projects\JMAD-Curated-List

# Add remote (replace YOUR-USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR-USERNAME/JMAD-Curated-List.git

# Verify remote
git remote -v

# Push to GitHub
git push -u origin main
```

**If you get authentication errors**:
- Use a Personal Access Token instead of password
- Or use SSH keys: https://docs.github.com/en/authentication/connecting-to-github-with-ssh

---

## Step 3: Verify Repository

1. Go to `https://github.com/YOUR-USERNAME/JMAD-Curated-List`
2. Verify files are visible:
   - ✅ README.md (should render with formatting)
   - ✅ curated-list.json
   - ✅ CONTRIBUTING.md
   - ✅ LICENSE
   - ✅ schema.json
   - ✅ .gitignore

---

## Step 4: Get Raw JSON URL

The raw JSON URL for the curated list will be:

```
https://raw.githubusercontent.com/YOUR-USERNAME/JMAD-Curated-List/main/curated-list.json
```

**Test the URL**:
```bash
curl https://raw.githubusercontent.com/YOUR-USERNAME/JMAD-Curated-List/main/curated-list.json
```

Should return the JSON content.

---

## Step 5: Update JMAD Installer

### Update Default Curated List URL

Edit `installer/models/curated_list.py`:

```python
# Line 18
DEFAULT_CURATED_LIST_URL = "https://raw.githubusercontent.com/YOUR-USERNAME/JMAD-Curated-List/main/curated-list.json"
```

### Update Documentation

Update README.md references to use your actual GitHub username.

### Update Sources Configuration

Edit `source/curated/sources.json`:

```json
{
  "sources": [
    {
      "name": "JMAD Official",
      "url": "https://raw.githubusercontent.com/YOUR-USERNAME/JMAD-Curated-List/main/curated-list.json",
      "enabled": true
    }
  ]
}
```

**Remove local test source** that was used for development.

---

## Step 6: Test Integration

1. Open JMAD Installer
2. Go to Settings tab
3. Verify curated source URL is correct
4. Click "Refresh Curated Lists"
5. Go to Applications tab
6. Verify 22 apps appear in curated section

**Expected behavior**:
- ✅ 22 apps loaded
- ✅ HTTP 200 response from GitHub
- ✅ Apps appear in grid
- ✅ Globe badges visible for apps without local files

---

## Step 7: Configure Repository Settings (Optional)

### Enable Issues
1. Go to repository Settings
2. Enable Issues for bug reports and feature requests

### Add Topics
Add topics to make repository discoverable:
- `windows`
- `installer`
- `curated-list`
- `package-manager`
- `silent-install`

### Add Repository Description
Settings → Description:
```
Official curated application list for JMAD Installer - 22 pre-configured apps with silent install arguments
```

### Add Website
Settings → Website:
```
https://github.com/YOUR-USERNAME/JMAD-Installer
```

---

## Updating the Curated List

### Making Changes

1. Edit `curated-list.json` locally
2. Update `last_updated` timestamp
3. Commit and push:

```bash
cd L:\Projects\JMAD-Curated-List

# Make changes to curated-list.json

git add curated-list.json
git commit -m "Update: Added new application XYZ"
git push origin main
```

### Version Updates

When making significant changes, update the version:

```json
{
  "version": "1.2.0",
  "last_updated": "2025-11-15T00:00:00Z",
  ...
}
```

---

## GitHub Pages (Optional)

If you want a pretty web page for the curated list:

1. Go to repository Settings → Pages
2. Source: Deploy from branch `main`
3. Folder: `/` (root)
4. Save

Your repository will be available at:
```
https://YOUR-USERNAME.github.io/JMAD-Curated-List/
```

The README.md will render as the homepage.

---

## CDN Acceleration (Optional)

For faster global access, you can use a CDN:

### jsDelivr (Free)

```
https://cdn.jsdelivr.net/gh/YOUR-USERNAME/JMAD-Curated-List@main/curated-list.json
```

**Benefits**:
- ✅ Faster downloads (CDN)
- ✅ Automatic caching
- ✅ Global distribution

**Update installer to use jsDelivr**:
```python
DEFAULT_CURATED_LIST_URL = "https://cdn.jsdelivr.net/gh/YOUR-USERNAME/JMAD-Curated-List@main/curated-list.json"
```

---

## Versioned Releases (Recommended)

Create GitHub releases for stable versions:

1. Go to repository → Releases
2. Click "Create a new release"
3. Tag: `v1.1.0`
4. Title: `v1.1.0 - GitHub Dynamic Resolution`
5. Description: Release notes
6. Publish release

Users can pin to specific versions:
```
https://raw.githubusercontent.com/YOUR-USERNAME/JMAD-Curated-List/v1.1.0/curated-list.json
```

---

## Troubleshooting

### "Repository not found"
- Verify repository is **public**
- Check repository name spelling

### "404 Not Found" for raw JSON
- Wait 1-2 minutes after push (GitHub cache)
- Verify branch is `main` (not `master`)
- Check URL spelling

### JMAD Installer can't fetch list
- Test URL in browser first
- Check internet connectivity
- Verify HTTP 200 response

### Authentication issues
- Use Personal Access Token
- Or configure SSH keys
- Or use GitHub Desktop app

---

## Post-Deployment Checklist

- [ ] Repository created and public
- [ ] Files pushed to GitHub
- [ ] Raw JSON URL accessible
- [ ] JMAD Installer updated with new URL
- [ ] Sources.json updated (removed local test source)
- [ ] Integration tested (22 apps load)
- [ ] Issues enabled on repository
- [ ] Topics added for discoverability
- [ ] README updated with correct URLs
- [ ] First release created (optional)

---

## Maintenance

### Weekly
- Check for application updates
- Update version-pinned apps
- Test download links

### Monthly
- Review GitHub issues
- Update documentation
- Check for new popular apps to add

### Quarterly
- Audit all download links
- Remove deprecated apps
- Update silent install arguments if changed

---

## Support

**Repository Issues**: https://github.com/YOUR-USERNAME/JMAD-Curated-List/issues
**Main Project**: https://github.com/YOUR-USERNAME/JMAD-Installer

---

**Next Steps**:
1. Create GitHub repository
2. Push code
3. Update JMAD Installer URLs
4. Test integration
5. Create v1.1.0 release

Good luck! 🚀
