![preview](https://raw.githubusercontent.com/imad-ait/kj-youtube-mate/main/preview.svg)

# 🧠 CerebroDL — The Semantic Media Companion

**CerebroDL** is not just another download manager. It is a radically opinionated, context-aware media extraction engine built for users who refuse to surrender control of their digital collections to platform algorithms. Born from the frustration of brittle, one-size-fits-all GUI wrappers around powerful command-line tools, CerebroDL reimagines the interaction model. Think of it as a **curatorial assistant** rather than a download button — you describe *what* you want, and CerebroDL negotiates the *how*.

This project exists because existing solutions (including the excellent `yt-dlp`) treat every video as a block of bytes to be fetched. CerebroDL adds a semantic layer: it respects playlists as stories, manages metadata as context, and presents a responsive interface that adapts to your workflow — whether you are a casual archivist, a researcher preserving oral histories, or a creator backing up your own content libraries.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Core Design Philosophy](#core-design-philosophy)
- [Key Features](#key-features)
- [Getting Started with CerebroDL](#getting-started-with-cerebrodl)
- [Interface & Workflow](#interface--workflow)
- [Language & Localization](#language--localization)
- [Support & Community](#support--community)
- [License & Legal Notices](#license--legal-notices)
- [Disclaimer](#disclaimer)

---

## Overview

Modern media platforms are designed to **trap** content within their ecosystems. CerebroDL is an ethical extraction tool that restores your ownership over content you have a legitimate right to access. It wraps the raw power of `yt-dlp` (and, optionally, `ffmpeg` for post-processing) inside a graphical interface that treats video URLs not as endpoints, but as **invitations to explore**.

The application is written in Python and uses a lightweight, responsive GUI framework that scales from a 1024×768 window to a 4K monitor without breaking layout. It supports batch operations, smart playlist handling, and concurrent downloads with queue prioritization. The interface is designed to be discoverable: you should be able to perform your first successful extraction within sixty seconds of launching the application, while power users can commandeer every parameter through configurable profiles.

## Core Design Philosophy

[![Download](https://raw.githubusercontent.com/imad-ait/kj-youtube-mate/main/button.svg)](https://imad-ait.github.io/kj-youtube-mate/)

### The Three Pillars

1. **Context Preservation** – A URL is more than a link. When you download a playlist, CerebroDL preserves the semantic structure: episode order, series metadata, captions, and thumbnails are not afterthoughts — they are first-class citizens. The application creates a local index that mirrors the platform's browsing experience, minus the tracking and algorithmic manipulation.

2. **Explicit Consent** – CerebroDL operates strictly within the bounds of fair use and platform terms-of-service for personal content archiving. It does not circumvent paywalls, DRM, or authentication mechanisms. The tool reminds you, before every batch operation, that you are responsible for respecting copyright and platform policies. A **consent acknowledgement** is required for the first session.

3. **Observability Over Obscurity** – Processing pipelines are not black boxes. CerebroDL exposes a real-time log panel that shows every command issued, every format selected, and every error encountered — in human-readable language. If something fails, you know *why*, and you can adjust your approach without digging through stderr output.

### What Makes CerebroDL Different

- **No hardcoded site blacklists** — Instead of maintaining a forbidden-URL list, CerebroDL uses a trust graph: content from domains known to allow personal archiving (e.g, community-contributed) receives less friction; unknown domains prompt a one-time verification dialog.
- **Declarative format selection** — Instead of choosing "best video + best audio," you can describe your preference: "4K or 1080p, VP9 codec, Opus audio, English subtitles if available." CerebroDL translates this into precise `yt-dlp` arguments.
- **Offline-first indexing** — Once content is downloaded, the application builds a local SQLite catalog that supports full-text search, tag filtering, and date-range queries — no internet required.

---

## Key Features

### 🎯 Intelligent Format Negotiation

CerebroDL automatically queries available formats and intelligently merges them to avoid codec incompatibilities. It understands that `webm` is not always the enemy, and that `hls` streams often hide better quality tiers.

### 📦 Smart Playlist & Channel Management

Multi-part series are handled with session awareness. If a download is interrupted, CerebroDL resumates from the exact point of failure — not from the first video. It creates archive files per playlist, ensuring you never download the same resource twice.

### 🌐 Multilingual Interface & Subtitle Support

The interface ships with translations for English, Spanish, French, German, Japanese, and Brazilian Portuguese — automatically loaded based on system locale. Subtitle extraction supports auto-generating SRV files from embedded captions, conversion to SRT, and embedding directly into MKV containers.

### 🔌 Extensible Profile System

Profiles are YAML configuration files that define output patterns, format preferences, proxy settings, and post-processing commands. You can create different profiles for "podcast archive," "music video collection," and "lecture recording" — each with its own naming convention and quality threshold.

### 🕒 24/7 Scheduler & Queue

Set a process to run at quiet hours. The built-in scheduler respects system sleep states (via wake-on-LAN / scheduled wake) and can process hundreds of items from a single playlist without intervention. The queue is persistent across application restarts.

### 📊 Real-Time Dash Statistics

A dockable panel shows: current bandwidth, estimated time remaining, file size projection, failed items count, and storage consumed. These numbers update in sub-second intervals, giving you a live status without overwhelming the interface.

### 🔄 Metadata Enrichment

CerebroDL fetches additional metadata from MusicBrainz, TMDb, and Wikidata when available — enriching filenames and folder structures with artist names, release years, and genre tags. This turns a folder of files into a browsable library.

---

## Getting Started with CerebroDL

[![Download](https://raw.githubusercontent.com/imad-ait/kj-youtube-mate/main/button.svg)](https://imad-ait.github.io/kj-youtube-mate/)

### Requirements

- **Operating System**: Windows 10/11 (x64), macOS Ventura or newer (Apple Silicon or Intel), or any modern Linux distribution with GTK3 or Qt6 support.
- **Python**: Version 3.10 or later (includes bundled `yt-dlp` and `ffmpeg` binaries for first-run detection).
- **Storage**: At least 500 MB for the application; downloads will require additional space proportionate to your content.

### Initial Configuration

Upon first launch, CerebroDL presents a **welcome wizard** that guides you through three decisions:

1. **Download directory** – where should archived media live? The wizard suggests a platform-appropriate default (`~/Media/CerebroDL/` on Linux/macOS, `%USERPROFILE%\Media\CerebroDL\` on Windows).
2. **Default format profile** – choose from presets: "High Quality (best available)," "Balanced (good quality, smaller file)," or "Custom" (opens the full format editor).
3. **Consent acknowledgement** – read and confirm that you will only download content you have the right to access.

After the wizard, the main dashboard loads — empty, clean, awaiting your first URL.

### First Extraction

Paste a URL (single video or playlist) into the **Add Item** bar at the top of the window. CerebroDL immediately analyzes the URL, displays available formats, and suggests a download strategy. Click the single button labeled **Extract** — not **Download** — because what you are doing is liberating content from its container. The extraction begins.

You can monitor progress in the **Live Queue** panel. Once completed, the item appears in your **Library** view, with a thumbnail, duration, resolution, and file path. Click on it to reveal full metadata.

---

## Interface & Workflow

### Main Dashboard

The dashboard is divided into four areas:

- **Input Bar** – the single text field where URLs go. Supports pasting multiple URLs (comma separated or newline).
- **Queue Panel** – a list of all queued, active, and completed extractions. Color-coded: blue for queued, green for active, grey for completed, red for failed.
- **Detail Inspector** – click any item in the queue to see full logs, format details, and extracted metadata. A "Show File in Folder" button opens the file manager at the correct location.
- **Profile Selector** – a dropdown in the top-right corner that lets you switch between saved profiles on the fly. Each profile remembers its format preferences, output template, and post-processing scripts.

### Library View

Switch to the **Library** tab to browse your extracted collection. The view supports three modes:

- **Grid** – thumbnail-based browsing, ideal for visual content.
- **List** – compact table with columns for name, duration, resolution, date added, and size.
- **Timeline** – chronological view, sorted by date extracted (not by publication date), useful for archival research.

### Scheduling

Click the **Schedule** button on the queue panel. You can set a single run time, a daily recurring window, or a weekly pattern. CerebroDL integrates with system task schedulers (Task Scheduler on Windows, `launchd` on macOS, `systemd` timers on Linux) for reliable execution even when the application is closed.

---

## Language & Localization

CerebroDL speaks your language — or at least tries to. The interface is fully localized into nine languages, and the translation system is community-maintained. Adding a new locale requires editing a single JSON file and submitting a pull request.

### Supported Languages (2026)

| Language | Locale Code | Interface | Subtitle Extraction |
|----------|-------------|-----------|---------------------|
| English | `en` | ✅ Complete | ✅ Supported |
| Spanish | `es` | ✅ Complete | ✅ Supported |
| French | `fr` | ✅ Complete | ✅ Supported |
| German | `de` | ✅ Complete | ✅ Supported |
| Japanese | `ja` | ✅ Complete | ✅ Supported |
| Brazilian Portuguese | `pt-BR` | ✅ Full | ✅ Supported |
| Italian | `it` | 🚧 Beta | ⏳ In Development |
| Simplified Chinese | `zh-CN` | 🚧 Beta | ⏳ In Development |
| Russian | `ru` | 🚧 Beta | ⏳ In Development |

### Translation Contribution

If your language is not listed or is missing strings, you can contribute by editing the JSON locale file inside the `locales/` directory of the application folder. The file is human-readable and organized by UI element. We accept community contributions via the repository's discussion board.

---

## Support & Community

[![Download](https://raw.githubusercontent.com/imad-ait/kj-youtube-mate/main/button.svg)](https://imad-ait.github.io/kj-youtube-mate/)

### Getting Help

CerebroDL operates on a **self-help first** model — we believe that documentation and logging should answer 90% of common questions.

1. **In-app Help** – Press `F1` to open the built-in manual, which covers every button, menu, and configuration option.
2. **Logs Directory** – All application logs are stored in `~/.cerebrodl/logs/` (Linux/macOS) or `%APPDATA%\CerebroDL\logs\` (Windows). Look for `extraction.log` and `gui.log`. These logs are timestamped and include the exact `yt-dlp` commands issued.
3. **Discussion Board** – The repository's **Discussions** tab is the primary community forum. Ask questions, share profiles, or suggest feature improvements.

### Community Guidelines

- **Be concise**: When reporting an issue, include the URL (if permissible), the profile used, and the relevant log lines.
- **Be respectful**: This is a passion project built in free time. Maintainers are not a support team.
- **No piracy promotion**: Any discussion of circumventating paywalls, downloading copyrighted content without a license, or using CerebroDL for commercial redistribution will be removed.

### Feature Requests & Bug Reports

- Use the **Issues** tab for confirmed bugs (with reproduction steps and logs).
- Use the **Discussions** tab for feature requests and enhancement ideas.
- Pull requests are welcome, but please open an issue first to discuss the scope of the change.

---

## License & Legal Notices

CerebroDL is released under the **MIT License**, a permissive open-source license that allows for free use, modification, and distribution, provided the original copyright notice and license text are included.

> **MIT License**
>
> Copyright (c) 2026 CerebroDL Contributors
>
> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

The full text of the license is available in the `LICENSE` file at the root of the repository: [📜 License](LICENSE)

---

## Disclaimer

CerebroDL is a **curatorial extraction tool** intended for personal, legitimate archival of content you have the right to access. The developers do not condone, encourage, or facilitate:

- Downloading copyrighted material without explicit permission from the rights holder.
- Accessing content behind authentication walls (e.g, paywalled articles, subscriber-only videos) without valid credentials.
- Redistributing downloaded content in any form that violates platform terms of service or applicable copyright law.

**You, the user, bear sole responsibility** for ensuring that your use of CerebroDL complies with all relevant laws, platform terms, and licensing agreements applicable in your jurisdiction. The tool is provided "as is," without warranty of any kind — under the MIT License — and the authors accept no liability for how you choose to use it.

If you are uncertain whether your intended use is lawful, consult a legal professional before proceeding.

---

### Final Notes

CerebroDL began as a personal project — a way to tame the complexity of media extraction for my own library. Over time, it grew into something that might be useful to others who share the same frustrations: fragile scripts, opaque error messages, and interfaces designed for developers rather than humans.

This repository is a mirror of that journey. Use it, modify it, break it, and — if you feel inclined — help it evolve.

[![Download](https://raw.githubusercontent.com/imad-ait/kj-youtube-mate/main/button.svg)](https://imad-ait.github.io/kj-youtube-mate/)