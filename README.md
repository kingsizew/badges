# Kingsize Badges

A high-resolution stream badge package for Nuvio, designed to remain clear
across mobile, desktop, and TV layouts.

The package contains **86 badges** covering source, resolution, quality,
visual formats, audio formats, channels, codecs, streaming services, and
special release tags.

![Nuvio Smart Tier List](docs/nuvio-smart-tier-list.png)

## Install

Use the raw JSON URL:

```text
https://raw.githubusercontent.com/kingsizew/badges/main/badge.json
```

You can also download [`badge.json`](badge.json) directly from this
repository.

## Color scale

| Tier | Color | Hex |
|---|---|---|
| T1 | Gold | `#FFD500` |
| T2 | Blue | `#176BE8` |
| T3 | Green | `#2EB853` |
| T4 | Orange | `#FF7300` |
| T5 | Red | `#E64141` |

Filters inside the Visual and Audio groups are ordered by tier so displayed
badges appear as gold, blue, green, orange, and red blocks rather than mixed
colors.

## Smart Visual hierarchy

The Visual group is not a single linear hierarchy.

### HDR family

```text
HDR10+ > HDR10 > HDR > SDR
```

Only the highest matching badge in this family is displayed.

### Independent Visual properties

- Dolby Vision
- HLG
- 10bit
- AI

These represent separate properties and may appear together with the selected
HDR-family badge.

## Smart Audio hierarchy

Audio uses independent branches. The highest matching badge in each branch is
displayed, while badges from different branches may appear together.

### Dolby branch

```text
Atmos TrueHD
Atmos Digital+
Atmos
TrueHD
DD+
DD
```

- `Atmos + TrueHD` becomes the combined **Atmos TrueHD** badge.
- `Atmos + DD+` becomes the combined **Atmos Digital+** badge.
- Standalone Atmos remains available when the carrier codec is not named.

### DTS branch

```text
DTS:X HD MA
DTS:X HD
DTS:X
DTS-HD MA
DTS-HD
DTS-ES
DTS
```

- `DTS:X + DTS-HD MA` becomes **DTS:X HD MA**.
- `DTS:X + DTS-HD` becomes **DTS:X HD**.
- Standalone DTS:X remains available when the carrier format is not named.

### Independent codec branch

```text
FLAC > Opus > AAC
```

This branch is independent from Dolby and DTS, allowing meaningful
multi-track information to remain visible.

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
```

| Category | Badges |
|---|---:|
| Special Tags | 4 |
| Media Source | 17 |
| Resolution | 9 |
| Quality | 12 |
| IMAX | 2 |
| Visual | 8 |
| Audio | 16 |
| Channels | 4 |
| Encoder | 5 |
| Streaming | 9 |
| **Total** | **86** |

## Image standard

Every image in [`badge-images`](badge-images) is the original PNG used by the
ordered badge configuration. No resizing, cropping, padding, redrawing, or
other visual transformation is applied, except for the standard IMAX badge,
which has 16 px of transparent left padding to prevent its first `I` from
touching the image edge.

## Direct image URLs

Badge image URLs use GitHub raw links:

```text
https://raw.githubusercontent.com/kingsizew/badges/main/badge-images/<category>/<badge-id>-original.png
```

The full ID-to-file mapping is available in
[`badge-images/manifest.json`](badge-images/manifest.json).

## Notes

- Badge matching is filename/metadata based.
- Multiple independent Visual or Audio properties can appear simultaneously.
- Combined immersive-audio badges suppress their redundant component badges.
- Product and service names, logos, and trademarks belong to their respective
  owners.
