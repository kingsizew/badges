# 🎨 Kingsize Nuvio Badges

A color-scaled and compatibility-aware stream badge package for
[Nuvio](https://github.com/NuvioMedia).

Stream names can contain a large amount of technical information, but showing
every detected tag makes the interface difficult to read. This package turns
that metadata into a compact set of recognizable badges so you can quickly
understand a stream's source, resolution, quality, visual format, audio format,
channel layout, encoder, and streaming service.

## About

Kingsize Nuvio Badges is a compact badge and formatter pack for Nuvio. It
turns stream metadata into clean, tier-aware visual badges while keeping
multiple style options for both colorful and minimal setups.

The Universal badge packs currently contain **100 badges**. Instant V2 packs contain those same badges plus **48 preferred-language badges** when used with marker-enabled formatters, for **148 V2 badges** total.

The package includes:

- seven visual badge styles;
- a five-color quality scale;
- automatic suppression of lower-tier duplicates;
- merged badges for formats that carry useful compatibility information;
- Smart Tier logic for Visual and Audio formats;
- informational Special Tags for alternate editions, corrected releases, and
  mastering variants;
- locally hosted PNG assets with stable GitHub Raw URLs;
- optional Instant V2 language badges generated from AIOStreams preferred-language markers.

> **Note:** For the best and smoothest Nuvio experience, you'll need a debrid service, and currently, [***TorBox***](https://torbox.app/subscription?referral=83bdd6a7-e951-4a82-8be4-99e5c6c97074) is the most affordable and highly recommended one. You can also share your Nuvio setup with your friends/family to use it together. If it's your first ever purchase, use my [***referral***](https://torbox.app/subscription?referral=83bdd6a7-e951-4a82-8be4-99e5c6c97074) and we both get +84 extra days on a yearly plan or +7 extra days on a monthly one.  
> **Referral Code:** 83bdd6a7-e951-4a82-8be4-99e5c6c97074

## 🚀 Installation

Choose the badge style you prefer, then choose the matching mode for your
formatter setup.

| Style | Universal JSON | Instant V2 JSON | Appearance |
|---|---|---|---|
| **Default Colored** | [`badge.json`](badge.json) | [`badge_v2.json`](badge_v2.json) | White icons/text with tier-colored borders |
| **Colored Outline** | [`colored_outline_badges.json`](colored_outline_badges.json) | [`colored_outline_badges_v2.json`](colored_outline_badges_v2.json) | Icons/text and borders use tier colors |
| **Solid** | [`solid_badges.json`](solid_badges.json) | [`solid_badges_v2.json`](solid_badges_v2.json) | Tier-filled badges with black icons/text |
| **Tinted** | [`tinted_badges.json`](tinted_badges.json) | [`tinted_badges_v2.json`](tinted_badges_v2.json) | Colored icons/text with tier-colored borders and soft tinted backgrounds |
| **Black** | [`black_badges.json`](black_badges.json) | [`black_badges_v2.json`](black_badges_v2.json) | Black-filled badges with white icons/text |
| **Mono White** | [`mono_white_badges.json`](mono_white_badges.json) | [`mono_white_badges_v2.json`](mono_white_badges_v2.json) | White-filled badges with black icons/text |
| **White** | [`white_badges.json`](white_badges.json) | [`white_badges_v2.json`](white_badges_v2.json) | White icons/text with white borders |

- **Universal JSONs** work with any formatter.
- **Instant V2 JSONs** are faster, but require one of the marker-enabled
  formatters below or a custom formatter using the marker template.

### Instant V2 — recommended with the included formatters

The V2 packages read lightweight structured markers supplied by the included
formatters. This avoids most expensive release-name matching and displays
badges at effectively instant speed.

```text
https://raw.githubusercontent.com/kingsizew/badges/main/badge_v2.json
https://raw.githubusercontent.com/kingsizew/badges/main/colored_outline_badges_v2.json
https://raw.githubusercontent.com/kingsizew/badges/main/solid_badges_v2.json
https://raw.githubusercontent.com/kingsizew/badges/main/tinted_badges_v2.json
https://raw.githubusercontent.com/kingsizew/badges/main/black_badges_v2.json
https://raw.githubusercontent.com/kingsizew/badges/main/mono_white_badges_v2.json
https://raw.githubusercontent.com/kingsizew/badges/main/white_badges_v2.json
```

The following ready-to-use formatters pass the same structured badge data while
offering different levels of visible detail:

- **Normal:** [View](normal_formatter.json) - [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/normal_formatter.json)
- **Minimalist with emojis:** [View](minimalist_with_emojis.json) - [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/minimalist_with_emojis.json)
- **Minimalist without emojis:** [View](minimalist_no_emojis.json) - [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/minimalist_no_emojis.json)
- **Tamtaro Instant:** [View](tamtaro_instant_formatter.json) - [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/tamtaro_instant_formatter.json)
- **Tamtaro Minimalist Instant:** [View](tamtaro_minimalist_instant_formatter.json) - [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/tamtaro_minimalist_instant_formatter.json)

The included marker-enabled formatters expose the same core technical markers to the badge matcher. The new marker template also includes 48 preferred-language markers. Language badges are generated from the languages selected in your AIOStreams configuration, so they should not clutter the badge row with languages you did not prefer.
**Note:** Only Tam’s default formatter exceeds the 5,000-character limit. If you want to use Tam’s default formatter with V2 badge packs, use the **[Kuu instance](https://aiostreams-nightly.206111.xyz/stremio/configure?menu=about&template=https://raw.githubusercontent.com/Tam-Taro/SEL-Filtering-and-Sorting/main/Tamtaro-All-Templates-for-AIOStreams.json)**.

#### Create your own Instant formatter

To make another custom formatter compatible with the Instant V2 badge packs:

1. Import the [Markers for Custom Formatters template](markers_for_custom_formatters.json)
   into the AIOStreams Custom Formatter. [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/markers_for_custom_formatters.json)
2. Add your custom formatter code **before** the existing marker codes in the
   corresponding `name` and `description` fields.
3. Keep each field below the formatter character limit and do not modify the
   invisible marker tokens.
   - If the `name` field exceeds 5,000 characters, move some marker blocks from
     `name` to the end of `description`, next to the existing description
     markers.
   - If the `description` field exceeds 5,000 characters, move some marker
     blocks from `description` to the end of `name`, next to the existing name
     markers.
   - If you do not need all language badges, you can delete languages you do not
     care about from the language marker replace-chain to free space.
4. Use one of the V2 badge packs in Nuvio:
   [`badge_v2.json`](badge_v2.json),
   [`colored_outline_badges_v2.json`](colored_outline_badges_v2.json),
   [`solid_badges_v2.json`](solid_badges_v2.json),
   [`tinted_badges_v2.json`](tinted_badges_v2.json),
   [`black_badges_v2.json`](black_badges_v2.json),
   [`mono_white_badges_v2.json`](mono_white_badges_v2.json), or
   [`white_badges_v2.json`](white_badges_v2.json).

### Universal — compatible with every formatter

Use the regular JSON files when using another formatter. These packages inspect
the filename, title, description, parsed metadata, addon-provided fields, and
their combined candidate. Their regex patterns have been compacted to minimize
overhead, but a small delay may remain because Nuvio evaluates every imported
badge rule against the available stream fields.

```text
https://raw.githubusercontent.com/kingsizew/badges/main/badge.json
https://raw.githubusercontent.com/kingsizew/badges/main/colored_outline_badges.json
https://raw.githubusercontent.com/kingsizew/badges/main/solid_badges.json
https://raw.githubusercontent.com/kingsizew/badges/main/tinted_badges.json
https://raw.githubusercontent.com/kingsizew/badges/main/black_badges.json
https://raw.githubusercontent.com/kingsizew/badges/main/mono_white_badges.json
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
They use a neutral light-blue style in the color-scaled packages, a white
outline style in the White Badge version, a white-filled monochrome style in
the Mono White version, and black or tinted variants in the matching visual
style packs. Their display order reflects practical relevance and
organization, not a quality hierarchy.

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
| Language | 48 | Instant V2 preferred-language badges from marker-enabled formatters |
| **Total** | **100 Universal / 148 V2** | |

Special-edition and streaming-service badges provide descriptive information,
while the ranked technical groups apply tier-based duplicate suppression. Language badges are included only in the Instant V2 packs and are driven by preferred-language markers from compatible formatters.

## ⚙️ Matching behavior

- Universal matching evaluates available filenames, titles, descriptions,
  parsed metadata, addon-provided fields, and their combined candidate.
- Instant V2 matching reads compact markers supplied by marker-enabled
  formatters, including preferred-language markers for the V2 language badges.
- Patterns are case-insensitive and recognize common release-name variations.
- Negative conditions suppress lower tiers and redundant component badges.
- Visual and Audio filters are stored in tier order for consistent display.
- Special Tags are ordered by practical relevance without applying tier logic.
- All visual style variants within each mode use identical matching rules; only
  their badge images, colors, borders, and fill styles differ.
- The JSON and image URLs are maintained together in this repository.

<!-- README -->
