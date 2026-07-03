# 🎨 Kingsize Nuvio Badges

A color-scaled and compatibility-aware stream badge package for
[Nuvio](https://github.com/NuvioMedia).

Stream names can contain a large amount of technical information, but showing
every detected tag makes the interface difficult to read. This package turns
that metadata into a compact set of recognizable badges so you can quickly
understand a stream's source, resolution, quality, visual format, audio format,
channel layout, encoder, and streaming service.

The package currently contains **100 badges** with:

- a five-color quality scale;
- automatic suppression of lower-tier duplicates;
- merged badges for formats that carry useful compatibility information;
- Smart Tier logic for Visual and Audio formats;
- informational Special Tags for alternate editions, corrected releases, and
  mastering variants;
- locally hosted PNG assets with stable GitHub Raw URLs.

## 🚀 Installation

Choose the badge mode that matches your formatter setup:

| Mode | Colored badges | White badges | Formatter support |
|---|---|---|---|
| **Instant V2** | [`badge_v2.json`](badge_v2.json) | [`white_badges_v2.json`](white_badges_v2.json) | Requires one of the three formatters below |
| **Universal** | [`badge.json`](badge.json) | [`white_badges.json`](white_badges.json) | Works with all formatters |

### Instant V2 — recommended with the included formatters

The V2 packages read lightweight structured markers supplied by the included
formatters. This avoids most expensive release-name matching and displays
badges at effectively instant speed.

```text
https://raw.githubusercontent.com/kingsizew/badges/main/badge_v2.json
https://raw.githubusercontent.com/kingsizew/badges/main/white_badges_v2.json
```

The following three companion formatters pass the same structured badge data
while offering different levels of visible detail:

- **Normal:** [View](normal_formatter.json) · [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/normal_formatter.json)
- **Minimalist with emojis:** [View](minimalist_with_emojis.json) · [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/minimalist_with_emojis.json)
- **Minimalist without emojis:** [View](minimalist_no_emojis.json) · [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/minimalist_no_emojis.json)

All three expose the same 78 active marker IDs to the badge matcher. Technical,
network, IMAX, and supported edition values are passed invisibly. Six Special
Tags—Hybrid, Criterion, Proper, Open Matte, Black & White, and True-Hue—remain
direct matches because AIOStreams does not expose equally broad structured
values for them; unsupported values remain visible in the formatter.

### Universal — compatible with every formatter

Use the regular JSON files when using another formatter. These packages inspect
the filename, title, description, parsed metadata, addon-provided fields, and
their combined candidate. Their regex patterns have been compacted to minimize
overhead, but a small delay may remain because Nuvio evaluates every imported
badge rule against the available stream fields.

```text
https://raw.githubusercontent.com/kingsizew/badges/main/badge.json
https://raw.githubusercontent.com/kingsizew/badges/main/white_badges.json
```

## 🌈 How the badge system works

Ranked technical badges use five color tiers:

**T1 Gold → T2 Blue → T3 Green → T4 Orange → T5 Red**

Gold represents the strongest or most premium formats, followed by Blue,
Green, Orange, and Red. When multiple tags from the same standard group are
detected, lower-tier matches are suppressed and the highest relevant badge is
displayed. Badges within the same color are also ordered from strongest to
weakest.

Visual and Audio need more context than a simple one-winner hierarchy, so they
use the Smart Tier logic explained below. Streaming-service badges retain their
brand colors, while special-edition badges are informational.

## 🧠 Smart Tier List

Visual and Audio formats are the most complex part of the package. They cannot
always be represented accurately by one simple quality ladder.

Some tags describe different technical properties, compatibility layers, codec
families, or playback paths. Hiding everything except one globally
"highest-quality" tag can remove information that is useful when choosing a
stream for a TV, computer, mobile device, soundbar, or home-theater receiver.

The Smart Tier List preserves useful compatibility information while
suppressing redundant component and fallback badges.

![Nuvio Smart Tier List](docs/nuvio-smart-tier-list.png)

## 🎨 Smart Visual hierarchy

Visual formats use one compatibility-aware hierarchy:

```text
> DV · HDR10+
> DV · HDR10
> DV · HDR
> Dolby Vision
> HDR10+
> HDR10
> HDR
> HLG
> 10bit
> SDR
> AI
```

### Merged Dolby Vision badges

When Dolby Vision and a compatible HDR layer are both detected, they are
represented by one merged badge:

| Detected formats | Displayed badge |
|---|---|
| Dolby Vision + HDR10+ | **DV · HDR10+** |
| Dolby Vision + HDR10 | **DV · HDR10** |
| Dolby Vision + generic HDR | **DV · HDR** |

These merged badges communicate both the Dolby Vision format and its HDR
compatibility information without displaying two separate Visual badges.

HLG, 10bit, SDR, and AI act as fallback results when no higher Visual format is
detected.

## 🎧 Smart Audio selection

Audio is evaluated through Dolby, DTS, and general codec logic instead of
forcing every format into one oversimplified hierarchy.

### Dolby branch

```text
> Atmos · TrueHD
> Atmos · Digital+
> Atmos
> TrueHD
> DD+
> DD
```

### DTS branch

```text
> DTS:X · HD MA
> DTS:X · HD
> DTS:X
> DTS-HD MA
> DTS-HD
> DTS-ES
> DTS
```

Each branch first selects its strongest matching format. Combined Atmos and
DTS:X badges replace their redundant component badges.

### FLAC, Opus, and AAC

```text
> FLAC
> Opus
> AAC
```

- **FLAC** is treated as a T2 lossless candidate and competes with the Dolby
  and DTS branch winners.
- **Opus** and **AAC** act as fallback codecs when no Dolby or DTS format is
  detected.
- If several meaningful Audio candidates are present, lower-priority results
  are suppressed.
- Equal-tier Dolby and DTS formats take priority over FLAC because they provide
  more specific device and home-theater compatibility information.

Examples:

| Detected formats | Displayed formats |
|---|---|
| Atmos TrueHD + DTS:X HD MA + FLAC | Atmos · TrueHD + DTS:X · HD MA |
| Atmos TrueHD + DTS-HD + FLAC | Atmos · TrueHD + FLAC |
| DD+ + DTS-HD + FLAC | DTS-HD + FLAC |
| DD+ + DTS-ES + FLAC | DD+ + FLAC |
| DTS + Opus | DTS |
| Opus + AAC | Opus |
| FLAC + Opus + AAC | FLAC |

## 🏆 Standard tier selection

Most badge groups use a traditional tier hierarchy. When several tags from the
same group are detected, lower-tier matches are suppressed and only the
highest relevant result is displayed.

Examples:

```text
Resolution: 4K > 1440p > 1080p > 720p > lower resolutions
Quality:    Remux > BluRay > WEB-DL > WEBRip > lower-quality sources
IMAX:       IMAX Enhanced > IMAX
Channels:   7.1 > 6.1 > 5.1 > 2.0
Encoder:    AV1 > HEVC > AVC > XviD > DivX
```

The same principle is used for ranked Remux, BluRay, and WEB media-source
profiles. This prevents combinations such as `4K + 1080p + 720p` or
`Remux + BluRay + WEB-DL` from producing unnecessary duplicate badges.

## 🎬 Special Tags

Special Tags describe corrected releases, alternate cuts, mastering changes,
and presentation variants that do not belong to the five-tier quality scale.
They use a neutral light-blue border in the color-scaled package and a white
border in the optional White Badge version. Their display order reflects
practical relevance and organization, not a quality hierarchy.

| Special Tag | Badge | Meaning |
|---|---|---|
| SeaDex | **SeaDex** | Identifies a curated SeaDex best or alternate release |
| Hybrid | **HYBRID** | Combines video, audio, subtitles, or other elements from multiple sources |
| Criterion Collection | **CRIT** | Identifies a Criterion Collection release |
| Proper | **PROPER** | Marks a corrected release that supersedes a flawed earlier release |
| Repack | **REPACK** | Marks a corrected reissue from the original release group |
| Remastered | **RMSTRD** | Uses a revised or improved audio/video master |
| Open Matte | **MATTE** | Uses expanded framing that reveals more image than the matted presentation |
| Regraded | **REGRD** | Uses modified color grading |
| Director's Cut | **DCUT** | Identifies the director's alternate cut |
| Extended | **EXT** | Identifies a longer or extended version |
| Uncut | **UNCUT** | Identifies a version presented without content being removed |
| Uncensored | **UNCENS** | Identifies an uncensored presentation |
| Black & White | **B&W** | Identifies a black-and-white presentation |
| True-Hue | **HUE** | Identifies a True-Hue Full Color presentation |
| Theatrical | **THTR** | Identifies the standard theatrical cut |

## 🧩 Included badge groups

| Group | Badges | Purpose |
|---|---:|---|
| Special Tags | 15 | SeaDex, corrected releases, alternate cuts, and presentation variants |
| Media Source | 17 | Ranked Remux, BluRay, and WEB profiles |
| Resolution | 9 | 4K through 144p |
| Quality | 12 | Remux, BluRay, WEB-DL, WEBRip, CAM, and others |
| IMAX | 2 | IMAX Enhanced and standard IMAX |
| Visual | 11 | Dolby Vision, HDR formats, HLG, 10bit, SDR, and AI |
| Audio | 16 | Dolby, DTS, FLAC, Opus, and AAC formats |
| Channels | 4 | 7.1, 6.1, 5.1, and 2.0 layouts |
| Encoder | 5 | AV1, HEVC, AVC, XviD, and DivX |
| Streaming | 9 | Streaming-service source badges |
| **Total** | **100** | |

Special-edition and streaming-service badges provide descriptive information,
while the ranked technical groups apply tier-based duplicate suppression.

## 🖼️ Badge images

All badge assets are stored in [`badge-images`](badge-images) and referenced by
stable GitHub Raw URLs:

```text
https://raw.githubusercontent.com/kingsizew/badges/main/badge-images/<category>/<filename>.png
```

Badge assets preserve their display proportions, composition, icon scale, and
text scale. Edges use transparent anti-aliasing for clean rendering on dark
interfaces.

The merged and standalone Dolby badges are rebuilt from vector-based artwork at
4x pixel density (320 px high). Nuvio displays them at the same visual size as
the other badges while the additional source pixels improve clarity on mobile,
desktop, TV, and high-DPI screens.

## 📁 Repository structure

```text
badge.json
white_badges.json
badge_v2.json
white_badges_v2.json
normal_formatter.json
minimalist_with_emojis.json
minimalist_no_emojis.json
badge-images/
├── special-tags/
├── media-source/
├── resolution/
├── quality/
├── imax/
├── visual/
├── audio/
├── channels/
├── encoder/
├── streaming/
└── manifest.json
docs/
└── nuvio-smart-tier-list.png
```

## ⚙️ Matching behavior

- Universal matching evaluates available filenames, titles, descriptions,
  parsed metadata, addon-provided fields, and their combined candidate.
- Instant V2 matching reads compact markers supplied by the three included
  formatters.
- Patterns are case-insensitive and recognize common release-name variations.
- Negative conditions suppress lower tiers and redundant component badges.
- Visual and Audio filters are stored in tier order for consistent display.
- Special Tags are ordered by practical relevance without applying tier logic.
- The colored and White Badge variants within each mode use identical matching
  rules; only their border colors differ.
- The JSON and image URLs are maintained together in this repository.

<!-- README -->
