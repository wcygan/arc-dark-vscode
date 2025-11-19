# Arc Dark Theme for VS Code - Implementation Plan

## Overview

This plan details how to port the Arc Dark theme from Zed to VS Code and publish it to the VS Code Marketplace.

**Source repository:** `/Users/wcygan/Development/zed-arc-dark-theme`

**Time estimate:**
- Theme creation: 15-30 minutes
- Publishing setup: 5 minutes
- Marketplace approval: 2-6 hours

---

## Step 1: Scaffold VS Code Extension

### Option A: Use Yeoman Generator (Recommended)

```bash
cd /Users/wcygan/Development/arc-dark-vscode
npm install -g yo generator-code
yo code
```

**Generator prompts:**
- Extension type: "New Color Theme"
- Theme import: "Start fresh"
- Theme name: "Arc Dark"
- ID: "arc-dark-theme"
- Description: "Arc Dark theme based on the popular Arc Dark color scheme"
- Publisher name: (your choice, can change later)

### Option B: Manual Setup

```bash
cd /Users/wcygan/Development/arc-dark-vscode
npm init -y
mkdir themes
```

---

## Step 2: Create Theme File

**File:** `themes/arc-dark-color-theme.json`

**VS Code theme schema:**
```json
{
  "type": "dark",
  "colors": {
    "editor.background": "#383c4a",
    "editor.foreground": "#d3dae3",
    "editor.lineHighlightBackground": "#404651",
    "editor.selectionBackground": "#2679db",
    "editor.inactiveSelectionBackground": "#1e61b0",
    "editorCursor.foreground": "#2679db",
    "editorWhitespace.foreground": "#505666",
    "editorLineNumber.foreground": "#9ba2ab",
    "editorLineNumber.activeForeground": "#d3dae3",

    "activityBar.background": "#2b2e39",
    "activityBar.foreground": "#d3dae3",
    "activityBar.activeBorder": "#2679db",

    "sideBar.background": "#383c4a",
    "sideBar.foreground": "#d3dae3",
    "sideBar.border": "#2b2e39",

    "statusBar.background": "#2b2e39",
    "statusBar.foreground": "#d3dae3",
    "statusBar.noFolderBackground": "#2b2e39",

    "titleBar.activeBackground": "#2b2e39",
    "titleBar.activeForeground": "#d3dae3",
    "titleBar.inactiveBackground": "#2b2e39",
    "titleBar.inactiveForeground": "#9ba2ab",

    "tab.activeBackground": "#383c4a",
    "tab.inactiveBackground": "#2b2e39",
    "tab.activeForeground": "#d3dae3",
    "tab.inactiveForeground": "#9ba2ab",
    "tab.border": "#2b2e39",

    "panel.background": "#383c4a",
    "panel.border": "#2b2e39",

    "input.background": "#404651",
    "input.foreground": "#d3dae3",
    "input.border": "#2b2e39",
    "input.placeholderForeground": "#9ba2ab",

    "dropdown.background": "#404651",
    "dropdown.foreground": "#d3dae3",
    "dropdown.border": "#2b2e39",

    "button.background": "#2679db",
    "button.foreground": "#ffffff",
    "button.hoverBackground": "#1e61b0",

    "list.activeSelectionBackground": "#2679db",
    "list.activeSelectionForeground": "#ffffff",
    "list.inactiveSelectionBackground": "#1e61b0",
    "list.hoverBackground": "#505666",
    "list.focusBackground": "#4e5467",

    "focusBorder": "#2679db",
    "contrastBorder": "#2b2e39"
  },
  "tokenColors": [
    {
      "scope": ["comment", "punctuation.definition.comment"],
      "settings": {
        "foreground": "#9ba2ab",
        "fontStyle": "italic"
      }
    },
    {
      "scope": ["keyword", "storage.type", "storage.modifier"],
      "settings": {
        "foreground": "#2679db"
      }
    },
    {
      "scope": ["string", "string.quoted"],
      "settings": {
        "foreground": "#98c379"
      }
    },
    {
      "scope": ["constant.numeric", "constant.language"],
      "settings": {
        "foreground": "#d19a66"
      }
    },
    {
      "scope": ["entity.name.function", "support.function"],
      "settings": {
        "foreground": "#61afef"
      }
    },
    {
      "scope": ["entity.name.type", "entity.name.class", "support.class"],
      "settings": {
        "foreground": "#e5c07b"
      }
    },
    {
      "scope": ["variable", "support.variable"],
      "settings": {
        "foreground": "#d3dae3"
      }
    },
    {
      "scope": ["invalid", "invalid.illegal"],
      "settings": {
        "foreground": "#e06c75"
      }
    }
  ]
}
```

**Reference source colors:**
- Background: `#383c4a` (main), `#404651` (secondary), `#474c5b` (tertiary)
- Borders: `#2b2e39`
- Accent: `#2679db` (primary), `#1e61b0` (inactive)
- Text: `#d3dae3` (primary), `#9ba2ab` (muted)
- Hover: `#505666`, `#4e5467`

**Color mapping source:** `/Users/wcygan/Development/zed-arc-dark-theme/references/arc-theme-idea-master/arc-theme-idea-dark/resources/arc_theme_dark.theme.json`

---

## Step 3: Configure package.json

**File:** `package.json`

```json
{
  "name": "arc-dark-theme",
  "displayName": "Arc Dark Theme",
  "description": "Arc Dark theme for VS Code based on the popular Arc Dark color scheme",
  "version": "1.0.0",
  "publisher": "your-publisher-id",
  "engines": {
    "vscode": "^1.80.0"
  },
  "categories": ["Themes"],
  "keywords": ["theme", "dark theme", "arc", "arc dark"],
  "repository": {
    "type": "git",
    "url": "https://github.com/username/arc-dark-vscode"
  },
  "license": "MIT",
  "contributes": {
    "themes": [
      {
        "label": "Arc Dark",
        "uiTheme": "vs-dark",
        "path": "./themes/arc-dark-color-theme.json"
      }
    ]
  }
}
```

**Update before publishing:**
- `publisher`: Set to your marketplace publisher ID (created in Step 5)
- `repository.url`: Set to your GitHub repo URL

---

## Step 4: Add Required Files

### LICENSE (Required)

Copy from Zed theme or create MIT license:

```
MIT License

Copyright (c) 2025 [Your Name]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

### README.md

```markdown
# Arc Dark Theme for VS Code

A dark theme for Visual Studio Code based on the popular Arc Dark color scheme.

## Installation

1. Open VS Code
2. Go to Extensions (Cmd+Shift+X)
3. Search for "Arc Dark Theme"
4. Click Install
5. Go to Code > Preferences > Color Theme
6. Select "Arc Dark"

## Screenshots

[Add screenshots here]

## Credits

Based on the Arc Dark theme originally designed for GNOME and adapted from the IntelliJ Arc Dark Theme.

## License

MIT
```

### icon.png (Optional but recommended)

**Requirements:**
- PNG format (SVG not allowed by vsce)
- Minimum 128x128 pixels
- Recommended 256x256 or 512x512

**Source:** Find Arc logo or create simple icon with Arc colors

---

## Step 5: Local Testing

### Test in Extension Development Host

```bash
cd /Users/wcygan/Development/arc-dark-vscode
code .
```

Press `F5` to launch Extension Development Host window. The theme will be available in the theme picker.

### Install Locally as VSIX

```bash
npm install -g @vscode/vsce
vsce package
code --install-extension arc-dark-theme-1.0.0.vsix
```

---

## Step 6: Create Azure DevOps Account & Publisher

### Create Personal Access Token (PAT)

1. Visit https://dev.azure.com
2. Create organization (free tier)
3. Click User Settings (top right) → Personal Access Tokens
4. Click "New Token"
5. Configure:
   - Name: "VS Code Marketplace"
   - Organization: "All accessible organizations"
   - Scopes: Custom defined → Marketplace → **Manage**
6. Click "Create"
7. **SAVE TOKEN SECURELY** (cannot view again)

**Documentation:** https://code.visualstudio.com/api/working-with-extensions/publishing-extension#get-a-personal-access-token

### Create Marketplace Publisher

1. Visit https://marketplace.visualstudio.com/manage
2. Sign in with Microsoft account (same as Azure DevOps)
3. Click "Create publisher"
4. Fill form:
   - **ID**: Unique identifier (e.g., `wcygan`, lowercase/hyphens only)
   - **Name**: Display name (e.g., "Will Cygan")
   - **Email**: Contact email
5. Click "Create"

**Update package.json** with publisher ID:
```json
{
  "publisher": "wcygan"
}
```

---

## Step 7: Publish to Marketplace

### Login with vsce

```bash
vsce login <publisher-id>
```

Enter PAT when prompted.

### Publish

```bash
vsce publish
```

This will:
1. Validate extension
2. Package as `.vsix`
3. Upload to marketplace
4. Auto-increment patch version

**Manual version control:**
```bash
vsce publish minor  # 1.0.0 → 1.1.0
vsce publish 1.2.0  # Specific version
```

### Verification

After publishing (2-6 hours for approval):
1. Visit https://marketplace.visualstudio.com/items?itemName=<publisher-id>.arc-dark-theme
2. Test installation from marketplace

---

## Step 8: Post-Publishing

### Update Extension

1. Make changes to theme
2. Update `version` in `package.json`
3. Run `vsce publish` again

### Monitor

- Marketplace page: https://marketplace.visualstudio.com/manage/publishers/<publisher-id>
- Download stats
- User ratings/reviews

---

## Reference Documentation

- **VS Code Color Theme Guide:** https://code.visualstudio.com/api/extension-guides/color-theme
- **Theme Color Reference:** https://code.visualstudio.com/api/references/theme-color
- **Publishing Extensions:** https://code.visualstudio.com/api/working-with-extensions/publishing-extension
- **Theme JSON Schema:** https://code.visualstudio.com/api/references/theme-color
- **vsce CLI:** https://github.com/microsoft/vscode-vsce

---

## Quick Reference Commands

```bash
# Install tools
npm install -g yo generator-code @vscode/vsce

# Create extension
yo code

# Test locally
code .
# Press F5

# Package
vsce package

# Install locally
code --install-extension arc-dark-theme-1.0.0.vsix

# Publish
vsce login <publisher-id>
vsce publish

# Update
vsce publish minor
```

---

## Troubleshooting

### "Publisher not found"
Run `vsce login <publisher-id>` first

### "Invalid publisher"
Update `publisher` field in `package.json` to match marketplace publisher ID

### "Cannot publish SVG images"
Replace any SVG icons with PNG (minimum 128x128)

### Theme not appearing
Ensure `contributes.themes` in `package.json` points to correct file path

### Local testing not working
Verify `vscode` engine version in `package.json` matches installed VS Code version

---

## File Structure

```
arc-dark-vscode/
├── themes/
│   └── arc-dark-color-theme.json
├── package.json
├── README.md
├── LICENSE
├── icon.png (optional)
└── CHANGELOG.md (optional)
```

---

## Color Palette Reference

**From:** `/Users/wcygan/Development/zed-arc-dark-theme/references/arc-theme-idea-master/`

| Element | Color | Usage |
|---------|-------|-------|
| Background Main | `#383c4a` | Editor, sidebar |
| Background Secondary | `#404651` | Inputs, inactive tabs |
| Background Tertiary | `#474c5b` | Panels |
| Border | `#2b2e39` | All borders, title bar |
| Accent Primary | `#2679db` | Focus, active selection |
| Accent Secondary | `#1e61b0` | Inactive selection |
| Text Primary | `#d3dae3` | Main text |
| Text Muted | `#9ba2ab` | Comments, disabled |
| Hover Light | `#505666` | List hover |
| Hover Dark | `#4e5467` | List focus |

**Syntax colors** can be refined by examining the IntelliJ theme at:
`/Users/wcygan/Development/zed-arc-dark-theme/references/arc-theme-idea-master/arc-theme-idea-dark/resources/arc_theme_dark.theme.json`
