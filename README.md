# Arabic dev tools

Small, focused tools for shipping Arabic software, mostly on Apple platforms. Each one is a
separate repository with its own tests and no dependencies unless it says otherwise.

## iOS and localization

| project | what it does |
| --- | --- |
| **[rtl-lint](https://github.com/hfip/rtl-lint)** | Finds `left`/`right` layout assumptions in Swift and storyboards that never mirror in Arabic. `rtl-lint migrate` writes a plan and opens a branch with one commit per rule group. |
| **[ArabicPlural](https://github.com/hfip/ArabicPlural)** | The six CLDR plural forms for Swift, including the `n % 100` cases everyone gets wrong. |
| **[xcstrings-audit](https://github.com/hfip/xcstrings-audit)** | Real coverage for `.xcstrings`, dropped `%@` placeholders, incomplete Arabic plurals, stale keys. |
| **[xcstrings-merge](https://github.com/hfip/xcstrings-merge)** | Moves legacy `.strings` translations into a String Catalog without overwriting reviewed text. |
| **[bidi-lab](https://github.com/hfip/bidi-lab)** | Splits a mixed Arabic/Latin line into runs, names the bidi bug, and applies the RLM fix. |
| **[rtl-previews](https://github.com/hfip/rtl-previews)** | One `#Preview` that renders the screen in English and Arabic side by side. |
| **[ArabicTextStyle](https://github.com/hfip/ArabicTextStyle)** | Line metrics for Arabic text: a bit more leading, more again when there is tashkeel. |

## Text and subtitles

| project | what it does |
| --- | --- |
| **[subfix](https://github.com/hfip/subfix)** | Repairs Arabic `.srt` files: encoding, double-decoded text, timings, RTL marks, watermark lines. Refuses to write when it cannot parse a cue. |
| **[subtitle-matcher](https://github.com/hfip/subtitle-matcher)** | Pairs subtitle files with videos by episode code, renames them next to the video. |
| **[arabic-slug](https://github.com/hfip/arabic-slug)** | URL slugs for Arabic, transliterated or kept in Arabic. |

## Apple TV and networks

| project | what it does |
| --- | --- |
| **[atv-deeplink](https://github.com/hfip/atv-deeplink)** | Builds and validates deep links for Infuse, VLC and YouTube on tvOS. |
| **[airplay-doctor](https://github.com/hfip/airplay-doctor)** | Checks interfaces, AirPlay ports and mDNS when the device does not show up. |

## Everything else

| project | what it does |
| --- | --- |
| **[env-doctor](https://github.com/hfip/env-doctor)** | Compares `.env` with `.env.example` and with the keys the code actually reads. |
| **[pr-size-labeler](https://github.com/hfip/pr-size-labeler)** | Labels pull requests by changed lines. |

## A typical pipeline

```yaml
- run: rtl-lint --format github Sources/        # layout assumptions
- run: xca --min-coverage 80 --strict Sources/   # translation coverage
- run: env-doctor --ci                           # configuration drift
```

```bash
subfix -r ~/Movies/Subs                          # the subtitles themselves
submatch ~/Media/Show ~/Downloads/subs --apply  # then the filenames
```

Each tool is MIT licensed, has tests, and a README that ends with what it will not do.
