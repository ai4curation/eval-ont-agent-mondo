# Porphyria gene-disease classification updates (issue #9703)

This PR implements the ClinGen General Inborn Errors of Metabolism GCEP proposal to update gene–disease classifications and inheritance patterns for 8 porphyria-associated genes (ALAS2, ALAD, HMBS, UROS, UROD, CPOX, PPOX, FECH). The proposal was provided as an Excel attachment from ClinGen EIM, with each row specifying a term to update or create.

## Changes

### Renamed existing terms (label + definition + synonyms updated)

| Term ID | Old name | New name |
|---------|----------|----------|
| MONDO:0010420 | X-linked erythropoietic protoporphyria | ALAS2-related erythropoietic protoporphyria |
| MONDO:0013000 | porphyria due to ALA dehydratase deficiency | ALAD-related hepatic porphyria |
| MONDO:0009902 | cutaneous porphyria | UROS-related erythropoietic porphyria |
| MONDO:0100498 | UROD-related inherited porphyria | UROD-related porphyria |
| MONDO:0800180 | CPOX-related hereditary coproporphyria | CPOX-related hepatic porphyria |
| MONDO:0008319 | protoporphyria, erythropoietic, 1 | FECH-related erythropoietic protoporphyria |

For each renamed term:
- The new label is added as a ClinGen-attributed EXACT synonym (with `OMO:0002001` qualifier)
- The previous label is kept as an EXACT synonym to preserve traceability
- The definition is replaced with the GCEP-supplied text; xref to `https://clinicalgenome.org/affiliation/40097/` and the issue URL
- A `term_tracker_item` (IAO:0000233) pointing to issue #9703 is added

### New terms

| Term ID | Name | Notes |
|---------|------|-------|
| MONDO:7770003 | HMBS-related hepatic porphyria | New parent, equivalent class = `hepatic porphyria` and `has material basis in germline mutation in some HMBS` |
| MONDO:7770004 | acute intermittent porphyria, nonerythroid variant | New child of MONDO:7770003 — currently unrepresented in OMIM as a standalone entry, definition from GCEP |
| MONDO:7770005 | PPOX-related hepatic porphyria | New parent, equivalent class = `hepatic porphyria` and `has material basis in germline mutation in some PPOX` |

### Re-parenting / lumping

Per GCEP Lumping & Splitting decisions:

- HMBS lump: `MONDO:0958224` (encephalopathy, porphyria-related), `MONDO:0958226` (leukoencephalopathy, porphyria-related), `MONDO:0008294` (acute intermittent porphyria) → added `is_a MONDO:7770003`.
- UROD lump: `MONDO:0015104` (porphyria cutanea tarda) → added `is_a MONDO:0100498`. `MONDO:0019799` (hepatoerythropoietic porphyria) is already a child of porphyria cutanea tarda, so it inherits the lump transitively.
- PPOX lump: `MONDO:0008297` (variegate porphyria) → added `is_a MONDO:7770005`. `MONDO:0957577` (variegate porphyria, childhood-onset) inherits transitively.
- CPOX lump: `MONDO:0007369` (hereditary coproporphyria) and `MONDO:0030048` (harderoporphyria) were already children of MONDO:0800180. After renaming, the parent CPOX class is now under `hepatic porphyria` (MONDO:0002520) rather than `inherited porphyria` to match the new label.

### Side effects

- **MONDO:0015104 (porphyria cutanea tarda)**: removed the legacy `excluded_subClassOf MONDO:0019142` (inherited porphyria) axiom. With the new `is_a MONDO:0100498` (which is itself an inherited porphyria), keeping the exclusion would be logically inconsistent. The editor note ("ORDO classifies as inherited but in fact many forms are inherited"; appears to be a typo in the original — many forms are *not* inherited) is preserved for context.
- **MONDO:0800180 (CPOX)**: parent changed from `inherited porphyria` (MONDO:0019142) to `hepatic porphyria` (MONDO:0002520) to reflect the new name. Inheritance is implicit via the gene-related child terms.

## Open question (flagged for review)

Sabrina Toro asked on the issue whether "erythropoietic porphyria" (used in the proposed UROS definition) should be a distinct new term, or whether it refers to "erythropoietic protoporphyria" (MONDO:0001676). 

My interpretation: in the porphyria literature, "erythropoietic porphyria" is a broader category encompassing both congenital erythropoietic porphyria (UROS) and erythropoietic protoporphyria (FECH/ALAS2). MONDO:0009902 already carries `erythropoietic porphyria` as an EXACT synonym (from DOID:13271, NCIT:C84697). I therefore left the parent hierarchy alone and applied only the rename. If the GCEP wants a separate grouping term, that should be tracked as a follow-up.

## Checklist

- [x] All renamed terms have new label as EXACT synonym (ClinGen-attributed)
- [x] All renamed terms retain previous label as a synonym
- [x] All renamed terms have updated definition with `https://clinicalgenome.org/affiliation/40097/` xref
- [x] All edited terms have `term_tracker_item` pointing to issue #9703
- [x] New terms use MONDO:777xxxx ID range (next available: 7770003–7770005)
- [x] New terms have logical definitions (equivalence axiom + has_material_basis_in_germline_mutation_in)
- [x] New terms have `dc:creator` annotation
- [x] HGNC gene IDs verified against existing usage in mondo-edit.obo (HMBS=4982, PPOX=9280, CPOX=2321, UROD=12591, UROS=12592, FECH=3647, ALAS2=397, ALAD=395) — all match prior `has_material_basis_in_germline_mutation_in` axioms on the corresponding disease terms
- [x] Lumping (is_a) relationships added per GCEP decisions
- [x] Source attribution on all new axioms

## Validation

- `obo-grep.pl` verifies each edited term parses and is retrievable from the file
- The file has 30,357 [Term] blocks with the 3 new IDs added (MONDO:7770003–7770005), continuing the existing series after MONDO:7770001 and MONDO:7770002
- `sh run.sh make NORM` was not run because docker is unavailable in this environment — please run normalization locally before merge
- Reasoner-based logical consistency check (e.g., `make test`) likewise needs to be run in the ODK container

## Notes for reviewer

- The "Split from sideroblastic anemia 1" annotation in the ALAS2 row of the spreadsheet is informational (sideroblastic anemia 1 has its own separate term). No action was taken on sideroblastic anemia.
- The OMIM entries for OMIM:614009 (mentioned in the GCEP table) etc. were not added as new xrefs since they were not explicitly requested; existing xrefs are retained.
- Inheritance patterns from the spreadsheet (XL, AR, semidominant) are encoded in the prose of each definition rather than as additional logical axioms, since the existing terms generally have `has_characteristic` axioms set already (e.g., MONDO:0010420 has `has_characteristic HP:0001417 ! X-linked inheritance`).

---
🤖 **Generated by claude agent**
- Runtime: `claude`
- Model: `claude-opus-4-7`
- Agent config: `ai4curation/mondo-agent-config@v3:.`
- Iteration: `1`
- Run: [View workflow run](https://github.com/ai4curation/eval-ont-agent-mondo/actions/runs/25819457086)
