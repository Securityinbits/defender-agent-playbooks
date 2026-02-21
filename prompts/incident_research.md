# Incident Research Prompt

You are my research assistant. Find **public, primary-source incident writeups** in **this year and last year** where the technique, tool, command, or behavior described in the **Target Paragraph** was **used in the wild** (not just tool intros).

## Target Paragraph
```
{{TARGET_PARAGRAPH}}
```
## How to interpret the Target Paragraph
- Extract key entities and variants: tool or framework names, commands, DLLs, user-agents, TTPs, MITRE techniques, file paths, registry keys, IOCs, and common aliases.
- Build a search plan using these variants and synonyms.

## SOURCES TO SEARCH (must include all)
- Google (open web)
- GitHub (repos, issues, advisories)
- X (x.com; posts that POINT to primary blog posts)
- Reddit (threads that POINT to primary blog posts)
- Chinese security sites: mp.weixin.qq.com, anquanke.com, freebuf.com, cn-sec.com
- Korean security sites: AhnLab ASEC blog, ESTsecurity ESRC blog, KrCERT/CC advisories, S2W LAB Intelligence
- Vendor TI blogs: Unit 42, The DFIR Report, Microsoft, Symantec (Broadcom), CrowdStrike, Mandiant, Cisco Talos, Securelist (Kaspersky), Trend Micro, ESET WeLiveSecurity, Check Point Research, Fortinet, SentinelLabs, WithSecure
- National or CERT advisories when they contain primary intrusion detail: CISA, JPCERT/CC, CERT-UA, CERT-PL, CERT-EU

## SCOPE AND RULES
- Only primary sources. If a primary is unavailable, include one reputable mirror and mark it as the primary (mirror).
- Timeframe: this and last year.
- What qualifies: Incident-backed usage such as an intrusion, campaign, or case study. Exclude generic tool overviews unless they contain a concrete incident.
- De-duplication: If multiple posts cover the same incident, keep the most authoritative or original one.
- For non-English titles, keep the original title and add a brief English gloss in parentheses if needed.
- Publish Date must be formatted as `D Mon, YYYY` (example: `5 Aug, 2025`).
- Titles: first column is the article title only, no outlet suffix.
- Source with link: second column is the outlet name only, hyperlinked exactly as
  `<a href="URL" target="_blank" rel="noopener noreferrer">Outlet Name</a>`
- Sort order: sort the table by Publish Date descending.

## OUTPUT (Markdown only)
Give me the download link for Markdown
| Source Title | Source (with link) | Publish Date |
|---|---|---|
| <TITLE_NO_OUTLET> | <a href="PRIMARY_URL" target="_blank" rel="noopener noreferrer">OUTLET_NAME</a> | D Mon, YYYY |
| ... |

## QUALITY CHECK BEFORE YOU ANSWER
- Verify each entry truly shows the Target Paragraph behavior used in an intrusion.
- Prefer the original publisher over news recaps.
- For Chinese posts, include WeChat originals if available. If paywalled or blocked, use a well-known mirror and note `(mirror)` after the outlet name.
- Keep the table to credible items only. A range of 3 to 10 rows is typical.