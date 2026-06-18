# Kingsize Badges

A stream badge package for Nuvio with **89 badges**, compact Visual/Audio
selection logic, color-tier ordering, and locally hosted PNG assets.

![Nuvio Compact Smart Tier List](docs/nuvio-smart-tier-list.png)

## Install

Use this raw JSON URL in Nuvio:

```text
https://raw.githubusercontent.com/kingsizew/badges/main/badge.json
```

## AIOStreams formatter

An optional Nuvio-oriented AIOStreams formatter is included at
[`aiostreams/nuvio-formatter.json`](aiostreams/nuvio-formatter.json).

Raw formatter URL:

```text
https://raw.githubusercontent.com/kingsizew/badges/main/aiostreams/nuvio-formatter.json
```

The formatter displays resolution, quality, editions, Visual/Audio tags,
languages, channels, subtitles, size, bitrate, source addon, indexer, release
group, and other available stream metadata in a compact layout.

## Color scale

| Tier | Color | Hex |
|---|---|---|
| T1 | Gold | `#FFD500` |
| T2 | Blue | `#176BE8` |
| T3 | Green | `#2EB853` |
| T4 | Orange | `#FF7300` |
| T5 | Red | `#E64141` |

Visual and Audio filters are ordered as Gold → Blue → Green → Orange → Red.

## Compact Visual hierarchy

Visual uses one global compatibility-aware hierarchy:

```text
DV · HDR10+
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

The merged badges preserve useful compatibility information without adding a
second Visual chip:

- Dolby Vision + HDR10+ becomes **DV · HDR10+**
- Dolby Vision + HDR10 becomes **DV · HDR10**
- Dolby Vision + generic HDR becomes **DV · HDR**

HLG, 10bit, SDR, and AI are fallback formats. They appear only when no
higher Visual format from the hierarchy is detected.

## Compact Audio selection

### Dolby branch

```text
Atmos · TrueHD
> Atmos · Digital+
> Atmos
> TrueHD
> DD+
> DD
```

### DTS branch

```text
DTS:X · HD MA
> DTS:X · HD
> DTS:X
> DTS-HD MA
> DTS-HD
> DTS-ES
> DTS
```

Each branch first selects its own best match.

### Codec behavior

```text
FLAC > Opus > AAC
```

- **FLAC** is a T2 lossless candidate and competes with the Dolby and DTS
  winners during Audio selection.
- **Opus** and **AAC** are fallback codecs. They appear only when neither a
  Dolby nor a DTS format is detected.
- When Dolby, DTS, and FLAC all match, lower-priority candidates are
  suppressed.
- Equal-tier Dolby/DTS formats take priority over FLAC because they provide
  more specific device and home-theater compatibility information.

Examples:

| Detected | Displayed |
|---|---|
| Atmos TrueHD + DTS:X HD MA + FLAC | Atmos · TrueHD + DTS:X · HD MA |
| Atmos TrueHD + DTS-HD + FLAC | Atmos · TrueHD + FLAC |
| DD+ + DTS-HD + FLAC | DTS-HD + FLAC |
| DD+ + DTS-ES + FLAC | DD+ + FLAC |
| DTS + Opus | DTS |
| Opus + AAC | Opus |
| FLAC + Opus + AAC | FLAC |

## Repository structure

```text
badge.json
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
aiostreams/
└── nuvio-formatter.json
```

| Category | Badges |
|---|---:|
| Special Tags | 4 |
| Media Source | 17 |
| Resolution | 9 |
| Quality | 12 |
| IMAX | 2 |
| Visual | 11 |
| Audio | 16 |
| Channels | 4 |
| Encoder | 5 |
| Streaming | 9 |
| **Total** | **89** |

## Image standard

The package preserves the original PNG artwork. The only intentional
exceptions are:

- the three custom merged Dolby Vision/HDR badges;
- the standard IMAX badge, which has 16 px of transparent left padding so its
  first `I` does not touch the image edge.

## Direct image URLs

Badge image URLs use GitHub Raw:

```text
https://raw.githubusercontent.com/kingsizew/badges/main/badge-images/<category>/<filename>.png
```

The complete mapping is available in
[`badge-images/manifest.json`](badge-images/manifest.json).

## Notes

- Matching evaluates the filename and supplied stream metadata.
- Combined badges suppress their redundant component badges.
- Product names, service names, logos, and trademarks belong to their
  respective owners.
