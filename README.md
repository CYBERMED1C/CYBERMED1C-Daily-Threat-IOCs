<!-- CYBERMEDIC-LIVE-STATUS:START -->
## Live status

🟡 **Published — source coverage limitations noted**

**Latest report:** [November 12, 2026](2026/11/12/11-12-26-iocs.md).

**Last successful IOC publication:** Confirmed 2026-11-12 15:33 UTC (minute precision).

**Overall status:** 114 validated IOCs are published. Research reviewed 45 substantive studies/records across 30 publisher groups. Source access gaps and retrospective observations are documented. Hunt queries received static review and were not executed on live security platforms.

**Daily schedule:** Active — 6:00 AM Pacific time (America/Los_Angeles).
<!-- CYBERMEDIC-LIVE-STATUS:END -->

> [!IMPORTANT]
> **TLP:CLEAR**
>
> Intelligence is drawn from publicly available sources. Use it for defensive investigation and assess every match in context.

# Daily-Threat-IOCs — Version 2.1.2

**Public threat intelligence. Traceable evidence. Practical hunts.**

Created and maintained under the **CYBERMEDIC** attribution at [CYBERMED1C/CYBERMED1C-Daily-Threat-IOCs](https://github.com/CYBERMED1C/CYBERMED1C-Daily-Threat-IOCs).

This project helps SOC analysts, threat hunters, incident responders and detection engineers turn public research into focused searches in Microsoft Defender XDR and Elastic Security. Each daily set brings together source context, structured indicators and ready-to-review hunting queries so an analyst can understand what a value represents before acting on a match.

Version 2.1.2 starts on **November 11, 2026**, with fresh research and an empty historical IOC baseline. No data, reports or Git history from the previous repository are imported. The established date folders and five-file daily structure remain the same.

[Open today's report](2026/11/11/11-11-26-iocs.md) · [Browse the archive](2026/)

## November 11, 2026: version 2.1.2 set

Today's revised set contains **42 unique indicators**, including **16 additions** after broader research. It covers Falcon / Antino, Citrus / Sn00py, FormBook, PureHVNC, njRAT, a macOS ClickFix chain and directly observed SSH exploitation. Each accepted value has a November 11 publication or a qualifying observation on the Los Angeles report day. Older activity and corroboration remain explicitly dated; publication today does not imply activity today.

| Indicator type | Count |
|---|---:|
| Domains | 6 |
| IP addresses | 4 |
| SHA256 file hashes | 19 |
| MD5 file hashes | 7 |
| SHA1 file hashes | 3 |
| URLs | 3 |
| **Total** | **42** |

| Open today's files | What to expect |
|---|---|
| [Daily intelligence report](2026/11/11/11-11-26-iocs.md) | Campaign context, defanged IOCs, evidence links and research limitations |
| [IOC table — CSV](2026/11/11/11-11-26-iocs.csv) | Flattened records for spreadsheets and security tools |
| [Structured records — JSON](2026/11/11/11-11-26-iocs.json) | Original values, hunt mappings, source evidence and collection metadata |
| [Microsoft Defender XDR hunt — KQL](2026/11/11/mde-hunt.kql) | Endpoint network, file and process searches |
| [Elastic Security hunt — ES\|QL](2026/11/11/elastic-hunt.esql) | Searches across compatible ECS fields in `logs-*` |

The extended two-pass review is complete. The live-status section records the confirmed publication state. Indicators retain their individual evidence, observation dates and false-positive notes; read the daily report before using them.

## Start hunting

1. **Read the report.** Check the indicator's campaign, role, source date and false-positive notes. Use the machine-readable files when importing exact values.
2. **Check your telemetry.** Confirm the tables, indexes, fields and retention available in your environment.
3. **Run the appropriate hunt.** Both queries use a rolling **30-day lookback** and return at most **500 matching records**, with the limit applied after IOC filtering.
4. **Investigate matches.** Review the process, file path, connection direction, timestamps and surrounding activity. Follow your normal response process before blocking or containing anything.

### Microsoft Defender XDR

Open the [KQL hunt](2026/11/11/mde-hunt.kql), copy the complete query into **Advanced hunting**, review its scope and run it against the intended environment. The current hunt uses `DeviceNetworkEvents`, `DeviceFileEvents` and `DeviceProcessEvents` from Microsoft Defender for Endpoint.

Domain indicators are compared with exact hostnames parsed from network telemetry. The documented exfiltration IP is matched as a remote destination. Observed SSH attack-source addresses match remote peers only when the endpoint local port is 22. Exact full URLs preserve their path and case. File and process hashes use their corresponding hash columns. The query does not expand domains to their parents or search for arbitrary substrings.

### Elastic Security

Open the [ES|QL hunt](2026/11/11/elastic-hunt.esql), copy the complete query into an **ES|QL query editor**, and review the `FROM logs-*` selection before running it. Narrow the index pattern to the intended telemetry and confirm that the fields used by `WHERE` are available with compatible mappings.

The current hunt uses `@timestamp`, `dns.question.name`, `destination.domain`, `url.domain`, `destination.ip`, `source.ip`, `destination.port`, `url.full`, and the applicable `file.hash.*` and `process.hash.*` fields. Hostnames and hashes are matched exactly after case normalization; destination and SSH source IPs use their distinct supported roles; SSH source matching also requires destination port 22. Full URLs match their exact path and case.

### What a query can miss

These hunts have been generated and checked for agreement with the accepted indicator set; **no live Defender or Elastic query execution is claimed**. Missing telemetry, unavailable tables, conflicting field types and permissions can affect execution or coverage. Defender SHA256 fields are often unpopulated, and browser extension resource files may not produce file-hash events. Elastic fields that are absent, multivalued or mapped differently may require an index or query adjustment.

A 30-day hunt does not retrieve March–May events outside that window. Any deliberate lookback change also depends on retained telemetry. No matches means no matches in the queried data and scope; it does not establish that an environment is free of compromise.

## Repository layout

Open the year, then the month, then the day. Each daily folder contains exactly five files:

```text
2026
└── 11
    └── 11
        ├── 11-11-26-iocs.md
        ├── 11-11-26-iocs.csv
        ├── 11-11-26-iocs.json
        ├── mde-hunt.kql
        └── elastic-hunt.esql
```

Browse one level at a time: [2026](2026/) → [11](2026/11/) → [11](2026/11/11/). Report dates use **America/Los_Angeles**. Evidence collection and publication timestamps use **UTC** with an explicit timezone.

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

The extended two-pass review covered **98 substantive reports, advisories or individual evidence records across 60 source organizations and four categories**. It met the normal 30-minute active-research minimum and added 28 source organizations in the second pass. Preparation and publication are excluded from research time; parallel reviews are not summed. The count includes older context, technical studies and patch advisories; it does not mean 98 new attacks occurred today.

The [daily report](2026/11/11/11-11-26-iocs.md) lists the reviewed evidence and material limits. Unavailable primary evidence, weak behavior, generic probing, diagnostic artifacts and shared infrastructure were excluded. A low or zero accepted count can still be valid after completed research; it does not establish a quiet threat day.

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
