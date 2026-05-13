# New term: MONDO:7770012 oocyte/zygote/embryo maturation arrest 16

Closes monarch-initiative/mondo#9855.

## Summary

Adds a new MONDO term for the PADI6-related female infertility / early embryonic arrest disorder (OMIM:617234). This OMIM entry was previously titled *preimplantation embryonic lethality 2* and was linked to the now-obsolete `MONDO:0014978`; OMIM has since renamed it to *oocyte/zygote/embryo maturation arrest 16*, putting it in the OZEMA series.

## Term

```
[Term]
id: MONDO:7770012
name: oocyte/zygote/embryo maturation arrest 16
def: "Any inherited oocyte maturation defect in which the cause of the disease is a mutation in the PADI6 gene. An autosomal recessive female infertility disorder characterized by early embryonic arrest." [PMID:27545678, PMID:29693651]
subset: omim {source="OMIM:617234"}
synonym: "early embryonic arrest" RELATED [PMID:27545678]
synonym: "inherited oocyte maturation defect caused by mutation in PADI6" EXACT [MONDO:patterns/disease_series_by_gene]
synonym: "OZEMA16" EXACT ABBREVIATION [MONDO:MEDGEN]
synonym: "PADI6-related oocyte/zygote/embryo maturation arrest 16 and maternal-effect disorder" EXACT [https://clinicalgenome.org/affiliation/40106] {OMO:0002001="https://w3id.org/information-resource-registry/clingen"}
synonym: "preimplantation embryonic lethality 2" RELATED [OMIM:617234]
synonym: "PREMBL2" RELATED ABBREVIATION [OMIM:617234]
xref: MEDGEN:934626 {source="MONDO:equivalentTo", source="MONDO:MEDGEN"}
xref: OMIM:617234 {source="MONDO:equivalentTo"}
xref: UMLS:C4310659 {source="MEDGEN:934626", source="MONDO:equivalentTo", source="MONDO:MEDGEN"}
is_a: MONDO:0014769 {source="OMIM:617234", source="PMID:27545678"} ! inherited oocyte maturation defect
intersection_of: MONDO:0014769 ! inherited oocyte maturation defect
intersection_of: has_material_basis_in_germline_mutation_in http://identifiers.org/hgnc/20449 ! PADI6
relationship: has_material_basis_in_germline_mutation_in http://identifiers.org/hgnc/20449 {source="OMIM:617234", source="PMID:27545678"} ! PADI6
property_value: http://purl.org/dc/terms/creator doi:10.1186/s13326-024-00320-3
property_value: IAO:0000233 "https://github.com/monarch-initiative/mondo/issues/9855" xsd:anyURI
```

## Rationale & decisions

- **Primary label.** The issue requested `PADI6-related oocyte/zygote/embryo maturation arrest 16 and maternal-effect disorder` (ClinGen preferred label). MONDO sibling terms (OZEMA 17–25, e.g. `MONDO:0957220`, `MONDO:0957230`, …, `MONDO:0980964`) all use the short OMIM-aligned name, so I used `oocyte/zygote/embryo maturation arrest 16` as the primary label and recorded the ClinGen-preferred long form as an `EXACT` synonym with the `OMO:0002001` (preferred label by community) qualifier pointing to ClinGen, per the CLAUDE.md guidance.
- **Parent.** As requested: `MONDO:0014769` (inherited oocyte maturation defect), the OMIM Phenotypic Series parent (OMIMPS:615774).
- **Design pattern.** Modelled with `disease_series_by_gene` — both the explicit `relationship: has_material_basis_in_germline_mutation_in` (with sources) and the equivalent `intersection_of` axioms, matching the pattern documented in `src/patterns/dosdp-patterns/disease_series_by_gene.yaml` and CLAUDE.md.
- **Gene identifier.** PADI6 → `http://identifiers.org/hgnc/20449`, verified via the HGNC REST API (`rest.genenames.org/fetch/symbol/PADI6`).
- **xrefs.** `OMIM:617234`, `MEDGEN:934626`, `UMLS:C4310659`, all confirmed via NCBI MedGen lookup for OMIM:617234. These were not present on the obsoleted predecessor `MONDO:0014978` except as `MONDO:obsoleteEquivalent` for OMIM; reattaching them as `MONDO:equivalentTo` here is appropriate since the OMIM record now matches the new MONDO concept.
- **Synonyms.**
  - `OZEMA16` EXACT ABBREVIATION (from MedGen, current OMIM abbreviation).
  - Legacy OMIM name `preimplantation embryonic lethality 2` and its abbreviation `PREMBL2` retained as RELATED (they describe the same OMIM entry pre-rename but the wording is no longer current OMIM nomenclature).
  - `early embryonic arrest` retained as RELATED (descriptive, not a clinical name).
  - Pattern synonym `inherited oocyte maturation defect caused by mutation in PADI6` added per design pattern.
- **References.**
  - PMID:27545678 — Xu et al., *Mutations in PADI6 Cause Female Infertility Characterized by Early Embryonic Arrest* (PMC5010645). Original gene-disease description.
  - PMID:29693651 — Qian et al., *Biallelic PADI6 variants linking infertility, miscarriages, and hydatidiform moles* (PMC6018785). Expanded phenotype.
- **Predecessor handling.** `MONDO:0014978` remains obsolete (not modified) with `xref: OMIM:617234 {source="MONDO:obsoleteEquivalent"}`; that qualifier signals the historical mapping and does not conflict with the new term's `MONDO:equivalentTo` claim.

## Checklist

- [x] Parent term `MONDO:0014769` exists and is appropriate
- [x] No existing live term covers OMIM:617234 (only the obsolete `MONDO:0014978` does, via `obsoleteEquivalent`)
- [x] New ID `MONDO:7770012` does not clash (`MONDO:7770011` was the prior highest 777-range ID)
- [x] HGNC ID for PADI6 verified (HGNC:20449)
- [x] OMIM / MedGen / UMLS IDs verified for OMIM:617234 (MEDGEN:934626, UMLS:C4310659)
- [x] PMIDs verified by fetching PMC5010645 and PMC6018785
- [x] Term parses cleanly (loaded the whole edit file through owltools, round-tripped to OBO, no errors)
- [x] Logical definition mirrors text definition (genus = inherited oocyte maturation defect; differentia = PADI6 mutation)
- [x] Issue link recorded in `IAO:0000233`
- [x] Creator signed (`doi:10.1186/s13326-024-00320-3`)

## Notes / caveats

- I was unable to run `make NORM` because Docker is not available in this environment; ODK normalization should be applied as part of the standard release pipeline. The stanza is hand-written to match existing formatting conventions and round-trips cleanly through owltools.
- `robot convert` is not installed locally either; syntactic validation was done by loading `src/ontology/mondo-edit.obo` (with the new term) through owltools and re-serialising it to OBO without errors.

---
🤖 **Generated by claude agent**
- Runtime: `claude`
- Model: `claude-opus-4-7`
- Agent config: `ai4curation/mondo-agent-config@v3:.`
- Iteration: `1`
- Run: [View workflow run](https://github.com/ai4curation/eval-ont-agent-mondo/actions/runs/25817239499)
