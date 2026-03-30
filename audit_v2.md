# WinLog v2 Audit -- Export Feature
**Auditor:** Nash (QA)
**Date:** 2026-03-29
**Scope:** v2-only checks (Export All Wins as Text)

---

## Check Results

### 1. Export button exists and wired
**PASS**

- Two export buttons in Insights tab (`#exportAllTextBtn` -- quick text export, `#exportBtn` -- modal with period/format).
- Both wired via `addEventListener` at lines 2493-2494.
- HTML at lines 914-924 is clean, SVG icons present.

### 2. Data collection from IndexedDB correct
**PASS**

- `exportAllWinsAsText()` (line 2253) calls `db.getAll()` with try/catch fallback to empty array.
- `getExportEntries()` (line 2194) also uses `db.getAll()` with fallback, plus period filtering (week/month/all).
- `db` is initialized as IndexedDB wrapper with `FallbackDB` (localStorage) fallback (lines 1153-1159).
- Sort order: `exportAllWinsAsText` sorts descending (newest first), `getExportEntries` sorts ascending. Both are valid for their use cases.

### 3. Text formatting clean
**PASS**

- `entriesToText()` (line 2209): structured header with name, separator, grouped by date with `formatDateRu()`, wins indented with `- `, categories in brackets, total count footer.
- `exportAllWinsAsText()` (line 2253): English month/day headers, bullet points, trailing newline trimmed. Clean and readable.
- Minor nit: `exportAllWinsAsText` uses English day/month names while `entriesToText` uses Russian (`formatDateRu`). Inconsistent but not a bug -- `exportAllWinsAsText` is the v2 "quick export" path.

### 4. Clipboard + download fallback
**FAIL**

- `exportAllWinsAsText()` only does download via Blob URL + `<a>` click (lines 2273-2279).
- No `navigator.clipboard.writeText()` call anywhere in the export flow.
- The spec says "Copy to clipboard or download .txt" -- clipboard path is missing entirely.
- `doExport()` also only downloads, no clipboard option.

### 5. escapeHtml / textContent on output
**PASS**

- Export preview uses `preview.textContent = entriesToText(entries)` (line 2233) -- safe, no innerHTML.
- Export-to-file writes plain text Blob -- no HTML context, no XSS vector.
- `exportAllWinsAsText` builds plain string with `w.text` directly into text file -- safe for plaintext output.
- `escapeHtml()` exists (line 996) and is used correctly in all innerHTML contexts elsewhere.

### 6. SW cache version bumped
**PASS**

- `sw.js` line 1: `CACHE_NAME = 'winlog-v2'` -- bumped to v2.
- Activate handler deletes old caches (lines 14-21).
- `skipWaiting()` + `clients.claim()` ensure immediate activation.

### 7. No regressions in existing features
**PASS**

- Export buttons are additive (new section in Insights tab, lines 914-925).
- Export modal (lines 945-964) is `hidden` by default, opened only on click.
- Escape key handler properly checks export modal state (line 2532).
- Focus trap applied correctly on modal open (line 2498).
- No existing event listeners or DOM structure modified.

---

## Summary

| # | Check                          | Result |
|---|--------------------------------|--------|
| 1 | Export button exists and wired | PASS   |
| 2 | IndexedDB data collection      | PASS   |
| 3 | Text formatting                | PASS   |
| 4 | Clipboard + download fallback  | FAIL   |
| 5 | escapeHtml / textContent       | PASS   |
| 6 | SW version bumped              | PASS   |
| 7 | No regressions                 | PASS   |

**Score: 6/7 (86%)**

**Delta from v1 baseline:** +1 feature (Export), -1 gap (no clipboard fallback).

---

## Action Items

1. **[MUST]** Add clipboard copy option to `exportAllWinsAsText()`:
   ```js
   try {
     await navigator.clipboard.writeText(text);
     showToast('Copied to clipboard!');
   } catch {
     // fallback to download (current behavior)
   }
   ```
   Or provide a "Copy" button alongside the "Export as Text" button.

2. **[NIT]** Harmonize language in export outputs -- `exportAllWinsAsText` uses English, `entriesToText` uses Russian. Pick one or respect a locale setting.
