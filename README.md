<!-- CYBERMEDIC-LIVE-STATUS:START -->
## Live status

**Latest published data:** November 17, 2026

- **Publication health:** 🟢 Published and verified on GitHub.
- **IOC validation health:** 🟢 Passed source, format, duplicate and cross-file checks for 124 validated IOCs.
- **Research collection health:** 🟡 Completed with documented source-access gaps.

| Latest published files — November 17, 2026 | What to expect |
|---|---|
| [Daily intelligence report](2026/11/17/11-17-26-iocs.md) | Campaign context, defanged IOCs, evidence links and research limitations |
| [IOC table — CSV](2026/11/17/11-17-26-iocs.csv) | Flattened records for spreadsheets and security tools |
| [Structured records — JSON](2026/11/17/11-17-26-iocs.json) | Original values, hunt mappings, source evidence and collection metadata |
| [Microsoft Defender XDR hunt — KQL](2026/11/17/mde-hunt.kql) | Endpoint network, file and process searches |
| [Elastic Security hunt — ES\|QL](2026/11/17/elastic-hunt.esql) | Searches across compatible ECS fields in `logs-*` |

Hunting queries passed static checks. They weren’t executed on live platforms.

**Status key** · 🟢 Green means required checks passed. 🟡 Yellow means usable output with specific limitations. 🔴 Red means required checks failed or are incomplete. ⚪ Gray means pending or not assessed.

**Daily schedule:** Active — 6:00 AM Pacific time (America/Los_Angeles).
<!-- CYBERMEDIC-LIVE-STATUS:END -->

> [!IMPORTANT]
> **TLP:CLEAR**
>
> Intelligence is drawn from publicly available sources. Use it for defensive investigation and assess every match in context.

# Daily-Threat-IOCs — Version 2.1.3

**Public threat intelligence. Traceable evidence. Practical hunts.**

Created and maintained under the **CYBERMEDIC** attribution as CYBERMED1C/CYBERMED1C-Daily-Threat-IOCs.

This project helps SOC analysts, threat hunters, incident responders and detection engineers turn public research into focused searches in Microsoft Defender XDR and Elastic Security. Each daily set brings together source context, structured indicators and ready-to-review hunting queries so an analyst can understand what a value represents before acting on a match.

The archive began on **November 11, 2026**, with fresh research and an empty historical IOC baseline. No data, reports or Git history from the previous repository are imported. Version 2.1.3 retains the established date folders and five-file daily structure.

The live-status section above links to the most recent published report, data files and hunts. Indicators retain their individual evidence, observation dates and false-positive notes; read that report before using them.

## Start hunting

1. **Read the report.** Check the indicator's campaign, role, source date and false-positive notes. Use the machine-readable files when importing exact values.
2. **Check your telemetry.** Confirm the tables, indexes, fields and retention available in your environment.
3. **Run the appropriate hunt.** Both queries use a rolling **30-day lookback** and return at most **500 matching records**, with the limit applied after IOC filtering.
4. **Investigate matches.** Review the process, file path, connection direction, timestamps and surrounding activity. Follow your normal response process before blocking or containing anything.

### Microsoft Defender XDR

Open `mde-hunt.kql` from the latest published set above, copy the complete query into **Advanced hunting**, review its scope and run it against the intended environment. The current hunt uses `DeviceNetworkEvents`, `DeviceFileEvents` and `DeviceProcessEvents` from Microsoft Defender for Endpoint.

Domain indicators are compared with exact hostnames parsed from network telemetry. IP indicators are matched according to their documented roles in the daily report. Exact full URLs preserve their path and case. File and process hashes use their corresponding hash columns. The query does not expand domains to their parents or search for arbitrary substrings.

### Elastic Security

Open `elastic-hunt.esql` from the latest published set above, copy the complete query into an **ES|QL query editor**, and review the `FROM logs-*` selection before running it. Narrow the index pattern to the intended telemetry and confirm that the fields used by `WHERE` are available with compatible mappings.

The hunt uses timestamps, hostname, IP, URL and file/process hash fields appropriate to the daily indicator set. Check the query for the exact ECS fields and mappings it requires. Hostnames and hashes are matched exactly after case normalization; IPs use their documented roles. Full URLs match their exact path and case.

### What a query can miss

These hunts have been generated and checked for agreement with the accepted indicator set; **no live Defender or Elastic query execution is claimed**. Missing telemetry, unavailable tables, conflicting field types and permissions can affect execution or coverage. Defender SHA256 fields are often unpopulated, and browser extension resource files may not produce file-hash events. Elastic fields that are absent, multivalued or mapped differently may require an index or query adjustment.

A 30-day hunt does not retrieve events outside that window. Any deliberate lookback change also depends on retained telemetry. No matches means no matches in the queried data and scope; it does not establish that an environment is free of compromise.

## Repository layout

Open the year, then the month, then the day. Each daily folder contains exactly five files:

```text
YYYY
└── MM
    └── DD
        ├── MM-DD-YY-iocs.md
        ├── MM-DD-YY-iocs.csv
        ├── MM-DD-YY-iocs.json
        ├── mde-hunt.kql
        └── elastic-hunt.esql
```

Browse one level at a time: year → month → day. Report dates use **America/Los_Angeles**. Evidence collection and publication timestamps use **UTC** with an explicit timezone.

| Daily file | Purpose |
|---|---|
| `MM-DD-YY-iocs.md` | Human-readable intelligence, sources, counts and coverage assessment |
| `MM-DD-YY-iocs.csv` | The established flattened IOC table |
| `MM-DD-YY-iocs.json` | Structured records with nested source evidence |
| `mde-hunt.kql` | Microsoft Defender XDR hunt |
| `elastic-hunt.esql` | Elastic Security hunt |

All five outputs derive from the same accepted set. The JSON preserves collection time, unassigned scores and full evidence objects; CSV provides a flattened table with the established fields. Unknown observation dates remain null in JSON and empty in CSV.

## How intelligence is collected

Research follows a rotating public-source roster: first-party security researchers, government and CERT advisories, contextual IOC records and official appendices. Reputable news helps discover leads; acceptance depends on evidence that can actually be retrieved and reviewed.

Collection focuses on original reports and their technical evidence. Each accepted indicator needs a documented malicious role, an exact supported scope and enough context to assess false positives. Generic feed membership or a score alone is insufficient.

Records retain source links, publication and observation dates, collection time and campaign context. Unsupported dates, attribution and scores remain unknown or unassigned. Values are checked for valid syntax and duplicates, and the report, data files and hunts are checked for agreement. Historical comparisons use only this archive; the previous repository is not used.

The **initial 2026-11-11 report** accepts evidence published that day or explicitly documenting observations on that date. This includes same-day publications with older activity, and exact indicator observations that fall on that Los Angeles day. Source update dates alone are not sufficient; supporting older research is explicitly labeled. For later runs, the primary freshness window is the preceding **48 hours**; sparse results can prompt a clearly labeled review of the preceding **seven days**. The window is not widened just to fill a count.

### Current research coverage

Each daily report records the reviewed studies, advisories, evidence records and source organizations, along with research time and material limitations. Preparation and publication are excluded from research time; parallel reviews are not summed. Review counts can include older context, technical studies and patch advisories; they do not measure new attacks.

The latest daily report lists the reviewed evidence and material limits. Unavailable primary evidence, weak behavior, generic probing, diagnostic artifacts and shared infrastructure were excluded. A low or zero accepted count can still be valid after completed research; it does not establish a quiet threat day.

## Understand the records

| Term or field | Meaning |
|---|---|
| `NEW` | First collected to this archive; it does not prove worldwide novelty or current activity |
| Source publication date | When the publisher released the supporting research |
| First / last seen | Indicator observation dates explicitly supported by the evidence; unknown values remain null |
| `collected_at` | When the evidence was collected for this project, in UTC |
| `original_ioc` | The original indicator value retained for traceability |
| `hunt_ioc` / `hunt_ioc_type` | The exact value and type used for matching; any deliberate scope change needs evidence and explanation |
| Confidence / acceptance score | Unassigned unless supported; the first set does not invent numerical scores |

Multiple hashes can describe components or alternate hashes of the same sample. Indicator counts therefore do not measure campaign counts, severity or prevalence. MD5 and SHA1 can be useful matching identifiers; they are not modern cryptographic integrity guarantees.

## Scope, false positives and safe use

**Treat a match as an investigation lead.** Consider the source's activity period, the indicator's role, legitimate administrative activity and surrounding endpoint or network evidence. Infrastructure can be shared, reassigned or taken down after publication. Exact source context matters before making a response decision.

Domains are not automatically widened to parent domains. An attacker source address is not automatically a malicious destination. Abused cloud or shared services require the exact supported path or scope; a provider root or shared public address must not be treated as broadly malicious without evidence for that exact value and role.

Human-readable network indicators are **defanged** using forms such as `[.]` and `hxxps`. Hashes remain readable. CSV, JSON, KQL and ES|QL retain the original matching values, so opening a machine-readable file can expose clickable infrastructure in some applications. **Do not browse to, ping, scan, download from or otherwise contact listed malicious infrastructure or samples.**

## Update cadence

The intended daily run is **6:00 AM Pacific time (America/Los_Angeles)**, following local daylight-saving time. A scheduled start is a research run time, not a guaranteed publication time. Live status at the top records the last confirmed publication, any temporary pause and material coverage limitations.
