# 🎨 Kingsize Nuvio Badges

Kingsize Nuvio Badges is a badge pack and formatter set for
[Nuvio](https://github.com/NuvioMedia). It turns stream metadata into compact
visual badges for source, resolution, quality, HDR, audio, channels, encoder,
streaming service, language, subtitles, and special tags.

The repo includes 7 badge styles, V1 badge packs for any formatter, Instant V2
badge packs for marker-enabled AIOStreams formatters, 5 ready-to-use formatters,
and a marker template for custom formatters.

> **Note:** For the best and smoothest Nuvio experience, you'll need a debrid service, and currently, [***TorBox***](https://torbox.app/subscription?referral=83bdd6a7-e951-4a82-8be4-99e5c6c97074) is the most affordable and highly recommended one. You can also share your Nuvio setup with your friends/family to use it together. If it's your first ever purchase, use my [***referral***](https://torbox.app/subscription?referral=83bdd6a7-e951-4a82-8be4-99e5c6c97074) and we both get +84 extra days on a yearly plan or +7 extra days on a monthly one.  
> **Referral Code:** 83bdd6a7-e951-4a82-8be4-99e5c6c97074

## Preview

Each preview diagram shows one badge pack and one formatter combination. The
top row shows the badges included in the pack, while the bottom row shows how
that pack looks when combined with a formatter on real stream results.

Use these previews to choose a ready-made badge pack + formatter combination,
or mix any badge pack with any included formatter to create your own setup.

![Tinted badges preview](docs/previews/tinted_badges.json.png)

Other previews:
[Colored Outline Badges](docs/previews/colored_outline_badges.json.png) ·
[Default Colored Badge](docs/previews/badge.json.png) ·
[Solid Badges](docs/previews/solid_badges.json.png) ·
[White Badges](docs/previews/white_badges.json.png) ·
[Mono White Badges](docs/previews/mono_white_badges.json.png) ·
[Black Badges](docs/previews/black_badges.json.png)

## Raw URLs

### Formatters

| Formatter | File | Raw URL |
|---|---|---|
| Normal | [normal_formatter.json](normal_formatter.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/normal_formatter.json) |
| Minimalist with emojis | [minimalist_with_emojis.json](minimalist_with_emojis.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/minimalist_with_emojis.json) |
| Minimalist without emojis | [minimalist_no_emojis.json](minimalist_no_emojis.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/minimalist_no_emojis.json) |
| Tamtaro Instant | [tamtaro_instant_formatter.json](tamtaro_instant_formatter.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/tamtaro_instant_formatter.json) |
| Tamtaro Minimalist Instant | [tamtaro_minimalist_instant_formatter.json](tamtaro_minimalist_instant_formatter.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/tamtaro_minimalist_instant_formatter.json) |
| Marker template for custom formatters | [markers_for_custom_formatters.json](markers_for_custom_formatters.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/markers_for_custom_formatters.json) |

### V1 Badge Packs

V1 packs work with any formatter and use Nuvio's normal badge matching.

| Style | File | Raw URL |
|---|---|---|
| Default Colored | [badge.json](badge.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/badge.json) |
| Colored Outline | [colored_outline_badges.json](colored_outline_badges.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/colored_outline_badges.json) |
| Solid | [solid_badges.json](solid_badges.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/solid_badges.json) |
| Tinted | [tinted_badges.json](tinted_badges.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/tinted_badges.json) |
| White | [white_badges.json](white_badges.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/white_badges.json) |
| Mono White | [mono_white_badges.json](mono_white_badges.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/mono_white_badges.json) |
| Black | [black_badges.json](black_badges.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/black_badges.json) |

### V2 Badge Packs

V2 packs are designed for the included formatters or a custom formatter based
on the marker template. They read compact hidden markers supplied by the
formatter for instant matching.

| Style | File | Raw URL |
|---|---|---|
| Default Colored | [badge_v2.json](badge_v2.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/badge_v2.json) |
| Colored Outline | [colored_outline_badges_v2.json](colored_outline_badges_v2.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/colored_outline_badges_v2.json) |
| Solid | [solid_badges_v2.json](solid_badges_v2.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/solid_badges_v2.json) |
| Tinted | [tinted_badges_v2.json](tinted_badges_v2.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/tinted_badges_v2.json) |
| White | [white_badges_v2.json](white_badges_v2.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/white_badges_v2.json) |
| Mono White | [mono_white_badges_v2.json](mono_white_badges_v2.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/mono_white_badges_v2.json) |
| Black | [black_badges_v2.json](black_badges_v2.json) | [Raw URL](https://raw.githubusercontent.com/kingsizew/badges/main/black_badges_v2.json) |

## How To Import

For formatters: copy the formatter raw URL, open the formatter section in
AIOStreams, and use **Import from URL**.

For badge packs: copy the badge pack raw URL, then open
**Nuvio Settings > Layout > Streams > Fusion Badge URLs** and add it there.

## V1 vs V2

- **V1 badge packs** work with any formatter. They rely on Nuvio's normal badge
  matcher and inspect the available stream fields directly.
- **V2 badge packs** require one of the included marker-enabled formatters, or a
  custom formatter using `markers_for_custom_formatters.json`. They use compact
  hidden markers for instant matching.
- **V2 adds Language and Subtitle badges.** These are generated only for the
  languages and subtitles you selected as preferred in AIOStreams, so the badge
  row stays focused instead of showing every detected option.
- **V1 does not include Language or Subtitle badges** because Nuvio's normal
  matcher fields do not provide consistent, dedicated language/subtitle data.
  Adding them to V1 would make the results incomplete and unreliable.

## Badge Logic

The badge packs contain **100 V1 badges**. V2 contains the same badges plus
**48 preferred-language badges** and **48 preferred-subtitle badges**, for
**196 V2 badges** total.

Ranked technical badge groups use five color tiers:

**T1 Gold > T2 Blue > T3 Green > T4 Orange > T5 Red**

For standard groups, higher-tier matches suppress lower-tier matches in the same
group. Visual and Audio badges use Smart Tier logic instead, so useful
compatibility information can stay visible when one simple winner would hide too
much detail.

![Nuvio Smart Tier List](docs/nuvio-smart-tier-list.png)

## Included Badge Groups

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
| Language | 48 | Instant V2 preferred-language badges |
| Subtitle | 48 | Instant V2 preferred-subtitle badges |
| Total | 100 V1 / 196 V2 | |

<!-- README -->
