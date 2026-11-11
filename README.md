<!-- CYBERMEDIC-LIVE-STATUS:START -->
## Live status

🟡 **Published — coverage limited**

**Latest report:** [November 11, 2026](2026/11/11/11-11-26-iocs.md).

**Last successful IOC publication:** Confirmed 2026-11-11 18:51:12 UTC.

**Overall health:** The 2026-11-11 set contains 26 IOCs. Research coverage is limited; see the daily report for sources, context and limitations.

**Daily schedule:** Active — 7:00 AM America/Los_Angeles.
<!-- CYBERMEDIC-LIVE-STATUS:END -->

> [!IMPORTANT]
> **TLP:CLEAR**
>
> Intelligence is drawn from publicly available sources. Use it for defensive investigation and assess every match in context.

# Daily-Threat-IOCs — Version 2.1.1

**Public threat intelligence. Traceable evidence. Practical hunts.**

Created and maintained under the **CYBERMEDIC** attribution at [CYBERMED1C/CYBERMED1C-Daily-Threat-IOCs](https://github.com/CYBERMED1C/CYBERMED1C-Daily-Threat-IOCs).

This project helps SOC analysts, threat hunters, incident responders and detection engineers turn public research into focused searches in Microsoft Defender XDR and Elastic Security. Each daily set brings together source context, structured indicators and ready-to-review hunting queries so an analyst can understand what a value represents before acting on a match.

Version 2.1.1 starts on **November 11, 2026**, with fresh research and an empty historical IOC baseline. No data, reports or Git history from the previous repository are imported. The established date folders and five-file daily structure remain the same.

[Open today's report](2026/11/11/11-11-26-iocs.md) · [Browse the archive](2026/)

## November 11, 2026: first version 2.1.1 set

The first set contains **26 unique indicators** from two primary reports published on **2026-11-11**. It covers Falcon / Antino browser espionage artifacts and Citrus / Sn00py intrusion activity. Exact indicator observation dates and present activity are unknown. The Falcon source describes March–May 2026 activity, so today's publication date must not be read as today's activity date.

| Indicator type | Count |
|---|---:|
| Domains | 5 |
| IP addresses | 1 |
| SHA256 file hashes | 16 |
| MD5 file hashes | 4 |
| SHA1 file hashes | 0 |
| URLs | 0 |
| **Total** | **26** |

| Open today's files | What to expect |
|---|---|
| [Daily intelligence report](2026/11/11/11-11-26-iocs.md) | Campaign context, defanged IOCs, evidence links and research limitations |
| [IOC table — CSV](2026/11/11/11-11-26-iocs.csv) | Flattened records for spreadsheets and security tools |
| [Structured records — JSON](2026/11/11/11-11-26-iocs.json) | Original values, hunt mappings, source evidence and collection metadata |
| [Microsoft Defender XDR hunt — KQL](2026/11/11/mde-hunt.kql) | Endpoint network, file and process searches |
| [Elastic Security hunt — ES\|QL](2026/11/11/elastic-hunt.esql) | Searches across compatible ECS fields in `logs-*` |

This set is **coverage limited**. The live-status section above records its publication state. All accepted indicators have single-source first-party evidence; independent corroboration and current malicious activity have not been confirmed. Read the report's coverage section before using the files.

## Start hunting

1. **Read the report.** Check the indicator's campaign, role, source date and false-positive notes. Use the machine-readable files when importing exact values.
2. **Check your telemetry.** Confirm the tables, indexes, fields and retention available in your environment.
3. **Run the appropriate hunt.** Both queries use a rolling **30-day lookback** and return at most **500 matching records**, with the limit applied after IOC filtering.
4. **Investigate matches.** Review the process, file path, connection direction, timestamps and surrounding activity. Follow your normal response process before blocking or containing anything.

### Microsoft Defender XDR

Open the [KQL hunt](2026/11/11/mde-hunt.kql), copy the complete query into **Advanced hunting**, review its scope and run it against the intended environment. The current hunt uses `DeviceNetworkEvents`, `DeviceFileEvents` and `DeviceProcessEvents` from Microsoft Defender for Endpoint.

Domain indicators are compared with exact hostnames parsed from network telemetry. The documented exfiltration IP is matched as a remote destination. File and process hashes use their corresponding hash columns. The query does not expand domains to their parents or search for arbitrary substrings.

### Elastic Security

Open the [ES|QL hunt](2026/11/11/elastic-hunt.esql), copy the complete query into an **ES|QL query editor**, and review the `FROM logs-*` selection before running it. Narrow the index pattern to the intended telemetry and confirm that the fields used by `WHERE` are available with compatible mappings.

The current hunt uses `@timestamp`, `dns.question.name`, `destination.domain`, `url.domain`, `destination.ip`, and the applicable `file.hash.*` and `process.hash.*` fields. Hostnames and hashes are matched exactly after case normalization; the IP is used only in its supported destination role.

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

The **initial 2026-11-11 report** accepts evidence published that day or explicitly documenting observations on that date. Every accepted value in this initial set comes from a report published that day. For later runs, the primary freshness window is the preceding **48 hours**; sparse results can prompt a clearly labeled review of the preceding **seven days**. The window is not widened just to fill a count.

### Current research coverage

For the first set, two passes reviewed **17 substantive reports, advisories or individual evidence records across 11 organizations and three categories**. Focused research lasted only a few minutes; the review windows overlap, so they do not represent separate blocks of elapsed research time. Exact active seconds were not recorded. This is a limited initial review, not full daily coverage. News searches supplied leads but no substantive news review was counted. Source access gaps and exclusions are documented in the [daily report](2026/11/11/11-11-26-iocs.md).

Some days may yield few accepted indicators or none. A verified zero-indicator day still requires completed research and an accurate coverage account. An empty template is not a completed report, and limited coverage cannot establish that threat activity was quiet.

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

The intended daily run is **7:00 AM America/Los_Angeles**, following local daylight-saving time. A scheduled start is a research run time, not a guaranteed publication time. Live status at the top records the last confirmed publication, any temporary pause and material coverage limitations.
