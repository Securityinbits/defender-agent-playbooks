# Incident Research Prompt: Generic (v3)

You are my research assistant. Find **public, primary-source incident writeups** in **this year and last year** where the technique, tool, command, or behavior described in the **Target Paragraph** was **used in the wild**.

## Target Paragraph
```
<PASTE a short paragraph describing the technique or behavior. Include any example commands, file paths, registry keys, user-agents, DLLs, or tool names if available.>
```

## How to interpret the Target Paragraph
- Extract key entities and variants: tool or framework names, commands, DLLs, user-agents, TTPs, file paths, registry keys, IOCs, common aliases, and ATT&CK mapping.
- Build a search plan using these variants, synonyms, and likely misspellings.

## Sources to search (must include all)
- Google (open web)
- GitHub (repos, issues, advisories)
- X (posts that **point to** primary sources)
- Reddit (threads that **point to** primary sources)
- Chinese security sites: mp.weixin.qq.com, anquanke.com, freebuf.com, cn-sec.com
- Korean security sites: AhnLab ASEC blog, ESTsecurity ESRC, KrCERT/CC advisories, S2W LAB Intelligence
- Vendor TI blogs: Microsoft, Mandiant, CrowdStrike, Cisco Talos, Unit 42, Securelist (Kaspersky), Trend Micro, ESET WeLiveSecurity, Check Point Research, Fortinet, SentinelLabs, WithSecure, Symantec (Broadcom)
- National or CERT advisories when they contain primary intrusion detail: CISA, JPCERT/CC, CERT-UA, CERT-PL, CERT-EU

## Operational notes
After opening each candidate source, if the page body is thin or contains cookie/consent strings (OneTrust, Cookiebot, TrustArc, Didomi) or dynamic JS messaging, try `/amp` or `/print`. If evidence is still missing or a pointer trail requires clicks, rerun that source in Agent mode and merge results.

## Search plan: run in this order

### 1) Mandatory site passes: precision layer
Run **site-scoped searches first** for each outlet category using the top entities from the Target Paragraph (tool names, command substrings, file paths, registry keys, user-agents, etc.). Use concise boolean groups.

- **DFIR Report:** `site:thedfirreport.com (<key entities>)`  
- **Vendors:** `site:security.microsoft.com` `site:unit42.paloaltonetworks.com` `site:mandiant.com` `site:crowdstrike.com` `site:blog.talosintelligence.com` `site:securelist.com` `site:trendmicro.com` `site:welivesecurity.com` `site:research.checkpoint.com` `site:fortiguard.com` `site:sentinelone.com` `site:withsecure.com` `site:broadcom.com`
- **National/CERTs:** `site:cisa.gov` `site:jpcert.or.jp` `site:cert.gov.ua` `site:cert.pl` `site:cert.europa.eu`
- **Korea:** `site:asec.ahnlab.com` `site:en.estsecurity.com OR site:esrc.co.kr` `site:krcert.or.kr` `site:s2wlab.com`
- **China:** `site:mp.weixin.qq.com` `site:anquanke.com` `site:freebuf.com` `site:cn-sec.com`

Notes:
- Keep DFIR Report in this pass for every task. It frequently publishes detailed, primary incident writeups that include commands and timelines.
- Include CISA joint advisories and similar national-level reports when they contain concrete intrusion details.

### 2) Exact-string and fragment queries: recall layer
Search the web for **verbatim strings** from the Target Paragraph:
- Quote key command substrings, paths, flags, DLL functions, user-agents, and registry keys. Examples: `"rundll32.exe comsvcs.dll"`, `"C:\\Windows\\NTDS\\ntds.dit"`, `"User-Agent: <value>"`, `"reg add <key>"`.
- Add likely variants and misspellings lifted from the Target Paragraph and common usage.

### 3) Social pointers: verification layer
- Search X and Reddit using the same literals plus keywords like `dfir`, `case study`, `incident`.
- Only use posts that **link to** a primary source. Do not cite the post itself unless the primary is unavailable.

### 4) GitHub sweep: tooling context
- Search repositories and issues for the tool names or command fragments to find **incident-backed** writeups in READMEs, advisories, or issue threads.
- Exclude pure tool intros that lack an intrusion context.

### 5) Non-English passes
- Translate 3–5 core terms from the Target Paragraph and rerun site-scoped searches on Chinese and Korean sources. Record any primaries found.

## Scope and rules
- Timeframe: **this year and last year**.
- What qualifies: Incident-backed usage such as an intrusion, campaign, or case study. Exclude generic tool overviews unless they include a concrete incident.
- De-duplication: If multiple posts cover the same incident, keep the most authoritative or original publisher.
- If a primary is blocked or paywalled, use a reputable mirror and mark `(mirror)` after the outlet name.

## Evidence gate: hard check
- Include an item **only if** the source shows the Target Paragraph behavior used in an intrusion.
- Save a one-line evidence snippet per item in a **hidden research log**: command line, file path, registry key, user-agent, or a sentence describing the action.
- Do not show the log in the final table unless requested.

## Output (Markdown only)
- Produce a **download link for Markdown** and the table below.
- Titles: first column is the article title only, no outlet suffix.
- Source with link: second column uses this exact format: `<a href="URL" target="_blank" rel="noopener noreferrer">OUTLET NAME</a>`
- Publish Date: `D Mon, YYYY`
- Sort by Publish Date **descending**.

| Source Title | Source (with link) | Publish Date |
|---|---|---|
| <TITLE_NO_OUTLET> | <a href="PRIMARY_URL" target="_blank" rel="noopener noreferrer">OUTLET_NAME</a> | D Mon, YYYY |
| ... |

### Quality check before you answer
- Verify each entry truly shows the behavior **used in the wild**.
- Prefer the **original publisher** over news recaps.
- For Chinese posts, include WeChat originals if available, or mark `(mirror)` on reputable mirrors.
- Keep the table to credible items only. Typical range: 3 to 10 rows.