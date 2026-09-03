# Caption Converter – SRT/WEBVTT

A single-page, browser-based tool for converting subtitle files between the `.srt` (SubRip) and `.vtt` (WebVTT) formats.

## What it is

A self-contained `caption-converter.html` file — no build step, no server, no dependencies. Open it in any modern browser and it works. All conversion happens client-side in JavaScript; files are never uploaded anywhere.

## What it does

- Converts **SRT → WEBVTT**: reads an uploaded `.srt` file, rewrites its timestamps and structure into valid WebVTT, and offers the result as a downloadable `.vtt` file.
- Converts **WEBVTT → SRT**: does the reverse, reading a `.vtt` file and producing a downloadable `.srt` file.

## Features

- Two independent conversion panels (SRT → VTT and VTT → SRT), each with its own file picker and submit button.
- Handles the core format differences automatically:
  - Comma vs. period millisecond separators in timestamps (`00:00:01,000` ↔ `00:00:01.000`).
  - The `WEBVTT` header line required by VTT files.
  - Sequential cue numbering required by SRT files.
  - Optional cue settings after VTT timestamps (e.g. `align:start`), preserved on SRT → VTT.
  - VTT-only inline tags (e.g. `<v Speaker>`), stripped on VTT → SRT.
  - Missing hour components in VTT timestamps (e.g. `01:02.500`), normalized to full `HH:MM:SS` on VTT → SRT.
- Output includes the converted filename and a "Download" button.
- Basic validation and error messages for empty files or files with no valid cues.
- Responsive layout with visible keyboard focus states.

## How it was built

A single HTML file containing:

- **HTML** — semantic structure for two upload forms and their output sections.
- **CSS** — plain, dependency-free styling (no frameworks or CDNs).
- **JavaScript (vanilla, no libraries)** — handles file reading (`FileReader`), parsing/conversion logic for both formats, and generates downloadable output using `Blob` and `URL.createObjectURL`.

Built as a single artifact by design, so it can be opened directly from disk or hosted as a static file with zero configuration.

## Usage

1. Open `caption-converter.html` in a browser.
2. Under the relevant section, choose your `.srt` or `.vtt` file.
3. Click **Convert to WEBVTT** or **Convert to SRT**.
4. Once conversion succeeds, click **Download** to save the converted file.
