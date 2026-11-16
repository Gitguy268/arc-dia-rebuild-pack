<div align="center">

# Arc and Dia rebuild pack

A feature inventory and rebuild specification for the Arc and Dia browsers, written so a developer or coding agent can rebuild them.

[What's inside](#whats-inside) · [How to use it](#how-to-use-it) · [Evidence policy](#evidence-policy) · [Limits](#limits) · [Contributing](#contributing)

![Entries](https://img.shields.io/badge/entries-116-6c5ce7) ![Researched](https://img.shields.io/badge/researched-2026--11--07-0984e3) ![Format](https://img.shields.io/badge/format-Markdown%20%2B%20JSON-636e72) ![License](https://img.shields.io/badge/license-MIT-2d3436)

</div>

Arc desktop stops working on **22 December 2026** ([official timeline](https://resources.arc.net/hc/en-us/articles/44412972248471-Arc-Sunset-Key-Dates-and-What-to-Expect)). This pack records what Arc and Dia do, so the features can live on in other browsers. It is a specification, not a browser and not recovered source code.

## What's inside

| File | What it is |
|---|---|
| [`arc-dia-rebuild-guide.md`](arc-dia-rebuild-guide.md) | The guide: 116 entries (40 Arc desktop, 50 Dia, 10 mobile, 16 shared foundations), each with documented evidence, a rebuild contract, state and storage, implementation notes and acceptance tests |
| [`feature-catalog.json`](feature-catalog.json) | The same entries as data, with stable feature IDs (`A01`, `D12`, `C05` and so on) and dated source links |
| [`coding-agent-handoff.md`](coding-agent-handoff.md) | A ready prompt for a coding agent, with the first vertical slice and the design rules |
| [`local-evidence.json`](local-evidence.json) | Read-only app bundle metadata (versions, build numbers, framework names, Info.plist hashes) of Arc 1.133.0 and Dia 1.56.0 |

## How to use it

1. Read the "Read this before selecting a target" section of the guide. It covers retired features and contradictions in the public docs.
2. Pick the feature IDs you want. The handoff suggests starting with `C01 C02 C03 C05 C06 C09 C13` and `A01 A02 A04 A05` (windows, tabs, pins, workspaces and storage groups).
3. Give the handoff prompt, the guide and the catalog to your agent or team, one vertical slice at a time.

Check that the JSON still parses after an edit:

```sh
python3 -m json.tool feature-catalog.json > /dev/null
```

## Evidence policy

- Only the **Documented evidence** paragraph of an entry is a summary of a cited public source.
- Everything under **Rebuild contract**, **State and storage**, **Implementation** and **Acceptance tests** is an independently proposed design. It does not describe how Arc or Dia work internally.
- `local-evidence.json` comes from reading app bundle metadata only. No browser profiles, cookies, history or credentials were read, and no app code was decompiled.

## Limits

- Two entries remain discovery tasks: **A39 TypeTravel** and **M03 pinch-to-summarize**. There wasn't enough public evidence to describe them.
- Nothing in the pack has been implemented or tested yet.
- Public documentation changes. Check entries against the build you're targeting before claiming parity.

<details>
<summary>Historical features that are included on purpose</summary>

Arc Notes (deprecated 18 April 2024), Arc's macOS Ask on Page (removed 28 August 2025) and Dia Memory (retirement started 24 September 2026) are in the pack. A rebuild may want the combined feature set, not only today's products. The guide marks each one as historical.

</details>

## Contributing

Corrections with a dated public source are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) and the [Code of Conduct](CODE_OF_CONDUCT.md).

## License

The pack's text and data are under the [MIT License](LICENSE). Arc and Dia are products of The Browser Company. This project is not affiliated with or endorsed by them, and their names and trademarks belong to them.
