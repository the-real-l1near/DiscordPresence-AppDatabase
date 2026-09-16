# Category Policy

This document defines how applications are categorized in the DiscordPresence application database.

The database is curated manually.

Accuracy is more important than coverage.

If an application's identity or category is uncertain, it should not be merged until sufficient evidence is available.

---

## Core Rule

An application's primary category is based on the product's core purpose.

It should answer:

> What is the main reason this product exists?

Do not classify an application based only on individual features it happens to include.

Examples:

- Visual Studio Code is a development application because its primary purpose is editing and developing software.
- Blender is a creative application because its primary purpose is 3D content creation.
- OBS Studio is a creative application because its primary purpose is recording and streaming media.
- Docker Desktop is a development application because its primary purpose is supporting software development and container workflows.

---

# Primary Categories

The initial database supports two primary categories:

- `development`
- `creative`

Additional primary categories may be introduced later if the database expands beyond the current scope.

---

# Development

Use `development` when the application's primary purpose is software development, programming, debugging, testing, deployment, infrastructure, or closely related technical workflows.

Supported subcategories:

## `ide`

Full integrated development environments.

Examples:

- Visual Studio
- IntelliJ IDEA
- Rider
- PyCharm

Use this when the product is positioned primarily as a complete development environment rather than a lightweight editor.

---

## `code-editor`

Code-focused editors that are lighter or more general-purpose than a traditional IDE.

Examples:

- Visual Studio Code
- Cursor
- VSCodium
- Sublime Text

---

## `version-control`

Applications primarily used to interact with version control systems or repositories.

Examples:

- GitHub Desktop
- GitKraken
- SourceTree
- Fork

---

## `database`

Database clients, database administration tools, and database-focused development tools.

Examples:

- DBeaver
- DataGrip
- HeidiSQL
- MySQL Workbench
- pgAdmin

---

## `api-client`

Applications primarily used to develop, test, inspect, or interact with APIs.

Examples:

- Postman
- Insomnia
- Bruno

---

## `container`

Applications primarily used to manage development containers or local container environments.

Examples:

- Docker Desktop
- Podman Desktop

---

## `game-engine`

Game engines and game-development environments.

Examples:

- Unreal Engine Editor
- Unity Editor
- Godot
- GameMaker
- Roblox Studio

Do not classify an ordinary game as `game-engine`.

---

## `embedded`

Development environments and tools primarily used for embedded systems or microcontroller development.

Examples:

- Arduino IDE
- PlatformIO

---

## `network-tool`

Applications primarily used for network inspection, debugging, proxying, or protocol analysis.

Examples:

- Wireshark
- Fiddler Everywhere
- Charles Proxy

---

## `terminal`

Terminal applications, shells, and terminal-oriented development tools.

Examples:

- Windows Terminal
- PowerShell
- Git Bash
- PuTTY

This subcategory should be used carefully because shell and terminal processes may require additional matching logic.

---

# Creative

Use `creative` when the application's primary purpose is creating, editing, producing, or publishing visual, audio, video, or other media content.

Supported subcategories:

## `image-editing`

Raster image editing and general image manipulation.

Examples:

- Adobe Photoshop
- GIMP
- Paint.NET
- Affinity Photo

---

## `digital-painting`

Applications primarily designed for drawing, painting, illustration, or digital art.

Examples:

- Krita
- Clip Studio Paint

Applications may include image-editing features without being classified as `image-editing`.

Use the product's primary purpose.

---

## `vector-design`

Vector graphics and vector illustration tools.

Examples:

- Adobe Illustrator
- Inkscape
- Affinity Designer
- CorelDRAW

---

## `3d`

Applications primarily used for 3D modeling, sculpting, texturing, rendering, or general 3D content creation.

Examples:

- Blender
- Autodesk Maya
- Autodesk 3ds Max
- Cinema 4D
- Houdini
- ZBrush
- Substance 3D Painter
- Substance 3D Designer
- Marmoset Toolbag
- Marvelous Designer
- MeshLab

---

## `cad`

Computer-aided design, engineering design, architecture, or technical modeling applications.

Examples:

- Autodesk AutoCAD
- Autodesk Fusion
- Autodesk Revit
- FreeCAD
- SketchUp

Some applications may overlap with general 3D workflows.

Use `cad` when engineering, architectural, technical, or manufacturing design is the product's primary purpose.

---

## `animation`

Applications primarily focused on animation production.

This category should only be used when animation is the product's primary identity rather than a secondary feature.

---

## `compositing`

Applications primarily used for compositing, motion graphics, visual effects, or post-production composition.

Examples:

- Adobe After Effects

---

## `video-editing`

Applications primarily used for video editing and video post-production.

Examples:

- Adobe Premiere Pro
- DaVinci Resolve
- Shotcut
- Kdenlive

---

## `publishing`

Applications primarily used for page layout, publishing, or document production.

Examples:

- Affinity Publisher

---

## `streaming`

Applications primarily used for live streaming, screen capture, or broadcasting.

Examples:

- OBS Studio

---

## `audio-production`

Applications primarily used for music production, audio editing, recording, or digital audio workstation workflows.

Examples:

- Audacity
- FL Studio
- Ableton Live
- REAPER
- LMMS
- MuseScore Studio

This may become a separate primary category in the future if the database expands significantly.

For database v1, it remains under `creative`.

---

# Category Selection Rules

When choosing a category and subcategory:

1. Prefer the product's official positioning and primary use case.
2. Prefer the purpose for which most users intentionally install the application.
3. Do not classify based on isolated features.
4. Do not classify based purely on executable names.
5. Do not mechanically derive categories from tags, votes, or download-site labels.
6. Do not create secondary classifications simply because an application can perform another type of task.
7. If two categories appear equally plausible, investigate further before merging the record.
8. If the current taxonomy does not fit an application cleanly, leave the application unsupported until the taxonomy is reviewed.

---

# Ambiguous Applications

Some applications serve multiple major workflows.

Examples include:

- Blender
- DaVinci Resolve
- Houdini
- Unreal Engine
- Adobe After Effects

The existence of multiple workflows does not mean the application needs multiple categories.

Choose the category that best represents the product's primary identity.

If this cannot be determined reliably, the record should not be merged yet.

---

# Matching Is Separate From Categorization

Application identity and application category are separate decisions.

A correct category does not make a weak match rule acceptable.

Likewise, a strong executable match does not prove that the category is correct.

Both must be reviewed independently.

---

# Unknown Is Better Than Incorrect

DiscordPresence should prefer an unknown application over an incorrect match.

The database should not attempt to maximize coverage at the expense of accuracy.

Do not merge a record if:

- the executable identity cannot be verified;
- the match rule conflicts with another application;
- the category is uncertain;
- the metadata is based only on assumption;
- the application is too poorly documented to identify reliably.

---

# Taxonomy Changes

Subcategories may be added, renamed, split, or merged as the database grows.

Taxonomy changes should be intentional and documented.

Do not add a new subcategory only to support a single unusual application unless there is a clear long-term reason for doing so.