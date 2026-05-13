# Obsolete MONDO:0023243 (glass-chapman-hockley syndrome), replace with MONDO:0011274 (Muenke syndrome)

Resolves #9798.

## Rationale

Glass-Chapman-Hockley syndrome was an n-of-1 historical term originally based on a single family (GARD:0002479, Orphanet:1535). The issue reporter and curator confirmed:
- The Orphanet record for `Craniosynostosis-dysmorphism-brachydactyly syndrome` (ORPHA:1535) is obsolete and was originally merged into Muenke syndrome (PMC5051481 / PMID:20108486).
- The SNOMED CT concept (SCTID:720814001) is retired per UMLS data.
- The phenotypic features (coronal craniosynostosis, midfacial hypoplasia, brachydactyly, autosomal-dominant inheritance) overlap with Muenke syndrome.

The term is therefore obsoleted with direct replacement by MONDO:0011274 (Muenke syndrome).

## Changes

**MONDO:0023243** reduced to a clean obsolete stanza:
- `name: obsolete glass-chapman-hockley syndrome`
- `property_value: IAO:0000231 MONDO:TermsMerged`
- `property_value: IAO:0000233` linking to issue #9798
- `is_obsolete: true`
- `replaced_by: MONDO:0011274`

**MONDO:0011274** (surviving Muenke syndrome) gains:
- Synonyms (RELATED for GARD-sourced; EXACT for "glass-chapman-hockley syndrome" with `[Orphanet:1535]` as evidence; EXACT for "craniosynostosis with facial dysmorphism and brachydactyly syndrome").
- `xref: Orphanet:1535 {source="GARD:0002479", source="MONDO:equivalentObsolete"}` — preserves historical mapping with appropriate obsolete-equivalent qualifier.
- `is_a: MONDO:0000426` (autosomal dominant disease) — applies to Muenke as well.
- `is_a: MONDO:0015469` craniosynostosis source qualifiers merged (`Orphanet:1535/inferred` added to existing ORCID).
- `property_value: IAO:0000233` linking to issue #9798.

## Items dropped intentionally

- `xref: SCTID:720814001` — SNOMED concept is retired per the issue; transferring as `equivalentTo` to Muenke would be inaccurate.
- `subset: obsoletion_candidate`, `subset: n_of_one`, `subset: inferred_rare`, and `property_value: IAO:0006012 "2026-02-01"` — obsoletion-tracking metadata specific to the obsoleted term; not appropriate on Muenke (well-described FGFR3-related syndrome, many families).
- The owltools-injected `synonym: "obsolete glass-chapman-hockley syndrome" EXACT [MONDO:0023243]` artefact.
- `property_value: seeAlso .../glass-chapman-hockley-syndrome` — the GARD page for the historical n=1 family; Muenke has its own GARD page already.
- The obsoleted term's GARD-sourced definition — Muenke retains its own concise definition.

## Validation checklist

- [x] `owltools --obsolete-replace` ran cleanly.
- [x] `make NORM` ran and was applied to `mondo-edit.obo`.
- [x] Obsolete stanza contains only allowed lines (id, name, `IAO:0000231 MONDO:TermsMerged`, `IAO:0000233` issue link, `is_obsolete`, `replaced_by`).
- [x] No obsoletion-tracking metadata leaked onto the surviving term.
- [x] No synonym on the surviving term cites the obsoleted MONDO ID.
- [x] No `alt_id` (per Mondo policy — no complete merges).
- [x] No other reference to MONDO:0023243 anywhere in the file outside its own stanza.
- [x] No duplicate synonym text across scopes on Muenke.
- [x] `robot convert` syntax check passes.
- [x] `robot verify` passes for: qc-misused-replaced-by, qc-obsoletion-reason, qc-deprecated-class-reference, qc-xref-without-precision, qc-duplicate-exact-synonym-no-abbrev, qc-proxy-merge-missing-preferred.

## Summary table

| What | From obsoleted | Status |
|------|---------------|--------|
| Synonyms | "craniosynostosis - dysmorphism - brachydactyly", "craniosynostosis brachydactyly", "craniosynostosis-dysmorphism-brachydactyly syndrome", "craniosynostosis with facial dysmorphism and brachydactyly syndrome", "glass chapman hockley syndrome", "glass-chapman-hockley syndrome" | transferred; evidence on "glass-chapman-hockley syndrome" repointed to `[Orphanet:1535]`; owltools-injected "obsolete glass-chapman-hockley syndrome" dropped |
| Xrefs | Orphanet:1535, SCTID:720814001 | Orphanet:1535 transferred (as `equivalentObsolete`); SCTID:720814001 dropped (retired) |
| Subsets | inferred_rare, n_of_one, obsoletion_candidate, rare | rare already on surviving; the other three dropped (obsoletion-tracking / n=1 specific) |
| `is_a` | MONDO:0000426 (autosomal dominant disease), MONDO:0015469 (craniosynostosis) | autosomal dominant transferred; craniosynostosis source merged into existing line |
| `intersection_of` | — | n/a |
| Relationships | — | n/a |
| Property values | IAO:0000233 (issue 9798), IAO:0006012 "2026-02-01", seeAlso GARD glass-chapman-hockley | issue link transferred; date dropped (obsoletion-tracking); GARD seeAlso dropped (historical) |
| Definition | GARD:0002479 description of glass-chapman-hockley | kept surviving Muenke definition (better established, matches issue intent) |
| Children rewired | — | none |
| New xrefs from issue | — | n/a |
| Obsoleted-stanza cleanup | — | reduced to id+name+TermsMerged+issue+is_obsolete+replaced_by |
| `alt_id` | — | none |

---
🤖 **Generated by claude agent**
- Runtime: `claude`
- Model: `claude-opus-4-7`
- Agent config: `ai4curation/mondo-agent-config@v3:.`
- Iteration: `1`
- Run: [View workflow run](https://github.com/ai4curation/eval-ont-agent-mondo/actions/runs/25816126783)
