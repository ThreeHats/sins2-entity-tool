# Sins 2 Entity Tool

A desktop GUI application for editing Sins of a Solar Empire II mod files—entities, research trees, localization, and more—without manually wrangling JSON.

> **⚠️ Beta Release** — Backup your mod folder before use. This tool is functional but still under active development.

[![Demo Video](https://img.shields.io/badge/▶_Demo_Video-YouTube-red)](https://youtu.be/2VGNgComdik?si=5GnYF6CmZ_XoJkFS) [![Latest Release](https://img.shields.io/github/v/release/ThreeHats/sins2-entity-tool)](https://github.com/ThreeHats/sins2-entity-tool/releases/latest)

---

## Why This Tool?

Modding Sins of a Solar Empire II involves editing deeply nested JSON files that reference game schemas, textures, sounds, and localized text across multiple directories. Mistakes are easy; feedback is slow.

**Sins 2 Entity Tool** provides:
- **Form-based editing** — Properties render as appropriate controls (spinboxes, checkboxes, dropdowns) based on the game's JSON schemas
- **Visual asset selection** — Browse and preview textures and hear sound files before linking them
- **Research tree visualization** — Edit tech trees graphically instead of tracing JSON references
- **Undo/Redo** — A command-stack system tracks changes so you can safely experiment
- **Live validation** — Required fields are bold; base-game values are italicized; read-only fields are greyed out

This is a community tool. For the official modding tools, see [StardockCorp/sins2modtools](https://github.com/StardockCorp/sins2modtools).

---

## Features

| Category | Capabilities |
|----------|--------------|
| **Entity Editing** | Form-based UI auto-generated from official JSON schemas; context menus for adding/removing properties |
| **Research Trees** | Visual node graph editor for research subjects across all domains |
| **Asset Browsing** | Texture preview, sound playback (via Pygame), file selectors for mod and base game assets |
| **Localization** | Inline editing of localized text keys and values |
| **Workflow** | Undo/Redo (Ctrl+Z/Y), drag-and-drop mod folder loading, automatic update checks |

---

## Quick Start

### Download (Windows)

1. Grab the `.exe` from the [Latest Release](https://github.com/ThreeHats/sins2-entity-tool/releases/latest)
2. Place it in any folder and run it
3. On first launch, configure your **base game folder** and **mod folder** paths in Settings

### Run from Source (All Platforms)

```bash
git clone https://github.com/ThreeHats/sins2-entity-tool.git
cd sins2-entity-tool
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
python main.py
```

Use `--dev` to skip update checks during development.

---

## Usage Overview

1. **Open a mod** — Click "Open Mod Folder" or drag-and-drop a mod directory onto the window
2. **Navigate tabs** — Entities, Research, Uniforms, and other game data are organized into tabs
3. **Edit properties** — Click any entity to load its schema-driven form; right-click for context actions
4. **Preview assets** — Texture fields show thumbnails; sound fields let you play audio before selecting
5. **Save** — Ctrl+S or the Save button; changes are written back to the mod's JSON files

### Research Tree Editor

- Switch domains using the buttons at the top
- Click a node to edit its research subject
- Right-click to create or delete subjects (creates/removes the underlying JSON file)

### Tips

- **Bold** = required field | *Italic* = inherited from base game | Grey = read-only
- Right-click inside entity data to add root-level properties
- Refresh the view if the UI gets out of sync after complex edits

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| GUI Framework | PyQt6 |
| Audio Playback | Pygame |
| Schema Validation | jsonschema |
| Update System | GitHub Releases API + requests |

---

## Project Structure

```
main.py             # Entry point; handles updates and launches GUI
entityTool.py       # Main window, schema rendering, asset selectors (~6500 lines)
research_view.py    # QGraphicsView-based research tree visualization
command_stack.py    # Undo/Redo command pattern implementation (~2500 lines)
version_checker.py  # GitHub release polling and download logic
style.qss           # Dark theme stylesheet
config.json         # Persisted user settings (paths)
```

---

## Building an Executable

```bash
pip install pyinstaller
python -m PyInstaller entity-tool.spec
```

Output lands in `dist/`.

---

## Known Limitations

- Context menus occasionally require a view refresh to appear correctly
- Large entities may take 1–2 seconds to load or refresh
- Excessive undo/redo can sometimes desync the view (refresh to fix)
- Player icons and portrait files are not yet fully supported

See [GitHub Issues](https://github.com/ThreeHats/sins2-entity-tool/issues) for the full list.

---

## Contributing & Support

- **Issues**: [GitHub Issues](https://github.com/ThreeHats/sins2-entity-tool/issues)
- **Roadmap**: [Project Board](https://github.com/users/ThreeHats/projects/6)
- **Community**: [Discord Server](https://discord.com/invite/sinsofasolarempire) → [Entity Tool Thread](https://discord.com/channels/266693357093257216/1329849082675462144)

---

## Acknowledgments

- Stardock and Ironclad Games for Sins of a Solar Empire II and the official mod tools
- The Sins modding community for testing and feedback
- PyQt6 and Pygame maintainers
