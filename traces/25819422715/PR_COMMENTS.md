# SCN5A-related cardiac rhythm disorder and cardiogenetic rhythm disorder (issue #9707)

Implements the ClinGen Hereditary Cardiovascular Disease GCEP request (affiliation 40104) to add an SCN5A umbrella disease term and a new monogenic-rhythm-disease parent, and to reorganize the affected children.

## New terms

### MONDO:7770003 — cardiogenetic rhythm disorder
- **def**: "A heterogeneous group of cardiac rhythm phenotypes with a monogenic etiology that include, but are not limited to, atrial fibrillation, sick sinus syndrome, progressive cardiac conduction disease, ventricular fibrillation, Brugada syndrome, long QT syndrome, short QT syndrome, tachycardia with fibrillation, etc." (sourced to ClinGen affiliation 40104; uses the revised wording from @LengUNC's follow-up comment).
- **parents**: `cardiac rhythm disease` (MONDO:0007263), `cardiogenetic disease` (MONDO:0100547).
- **logical definition**: `cardiac rhythm disease` and `has_characteristic` some `inherited` (MONDO:0021152). This mirrors the equivalence axiom for `cardiogenetic disease` so the new term sits cleanly underneath both parents.
- **term_tracker_item**: github.com/monarch-initiative/mondo/issues/9707.

### MONDO:7770004 — SCN5A-related cardiac rhythm disorder
- **def**: revised definition from @LengUNC's follow-up comment (multifocal ectopic Purkinje-related premature contractions removed).
- **parent**: `cardiogenetic rhythm disorder` (MONDO:7770003) only. The two other parents listed in the request (`cardiogenetic disease`, `cardiac rhythm disease`) are entailed via MONDO:7770003 and were left for the reasoner.
- **logical definition** (disease_series_by_gene pattern): `cardiogenetic rhythm disorder` and `has_material_basis_in_germline_mutation_in` some `SCN5A` (`http://identifiers.org/hgnc/10593`). The HGNC ID for SCN5A was verified against existing SCN5A-related MONDO terms.
- **term_tracker_item**: github.com/monarch-initiative/mondo/issues/9707.

## Reparented existing terms

Added `is_a: MONDO:7770004 ! SCN5A-related cardiac rhythm disorder` to the five SCN5A-specific phenotypes:
- MONDO:0013530 atrial fibrillation, familial, 10
- MONDO:0024562 sick sinus syndrome 1
- MONDO:0011376 ventricular fibrillation, paroxysmal familial, type 1
- MONDO:0011377 long QT syndrome 3
- MONDO:0011001 Brugada syndrome 1

Added `is_a: MONDO:7770003 ! cardiogenetic rhythm disorder` to the family-level rhythm terms:
- MONDO:0014500 atrial conduction disease
- MONDO:0015263 Brugada syndrome
- MONDO:0018054 familial atrial fibrillation
- MONDO:0012061 familial sick sinus syndrome
- MONDO:0019490 progressive familial heart block
- MONDO:0000453 short QT syndrome
- MONDO:0008648 ventricular tachycardia, familial
- MONDO:0100234 paroxysmal familial ventricular fibrillation

Existing parents were preserved (per the project's policy of not removing parents unless explicitly requested). The reasoner will mark anything redundant.

## Excluded children

- **atrioventricular block (MONDO:0000465)** — not added under cardiogenetic rhythm disorder, following @katiermullen's curator note that this term does not necessarily have a monogenic etiology.
- The four "Phenotypes EXCLUDED but still associated with SCN5A" listed in the issue (sudden infant death syndrome susceptibility, heart block nonprogressive, heart block progressive type IA, dilated cardiomyopathy 1E) were not added as children of MONDO:7770004.

## Decisions and clarifications

- **"ventricular fibrillation, familial (MONDO:0011376)" in the request**: MONDO:0011376 is actually the SCN5A-specific subtype ("ventricular fibrillation, paroxysmal familial, type 1"); the only generic family-level term is MONDO:0100234 ("paroxysmal familial ventricular fibrillation"). Other entries in the same list (e.g., familial atrial fibrillation MONDO:0018054) are generic family-level terms, so MONDO:0100234 was attached as the direct child of MONDO:7770003. MONDO:0011376 still inherits cardiogenetic rhythm disorder transitively via MONDO:7770004. Flagged in the issue comment for confirmation.
- **Inheritance not in the logical definition for SCN5A-related term**: the request mentions autosomal dominant inheritance, but several SCN5A children include autosomal-recessive forms (e.g., SSS1 / OMIM:608567 has an autosomal-recessive synonym). Inheritance is retained in the textual definition but not in the equivalence axiom, so the term covers all reported SCN5A rhythm phenotypes.
- **Creator/source**: ClinGen affiliation URL (`https://clinicalgenome.org/affiliation/40104/`) used as the source on the new term, on the new parents, and on the new is_a relationships of reparented children, consistent with similar GCEP-attributed terms (e.g., MONDO:0700349 ACTN2-related cardiac and skeletal myopathy). No `dc:creator` ORCID was added since no individual curator ORCID was identified in the issue.

## Validation

- Verified all referenced MONDO IDs (parents and children) by lookup in `src/ontology/mondo-edit.obo`.
- Verified the HGNC identifier for SCN5A (10593) by cross-referencing existing SCN5A-related terms.
- Followed the `disease_series_by_gene` DOSDP pattern for MONDO:7770004 (`src/patterns/dosdp-patterns/disease_series_by_gene.yaml`).
- ROBOT/owltools were not available in this environment, so the standard `robot convert` validation and `make NORM` normalization could not be executed. The file passes basic OBO structural checks (every `[Term]` stanza has an id; new stanza placement preserved by `obo-checkin.pl`). A NORM step is expected to run in CI.

## Checklist
- [x] New term IDs do not clash (greppd `MONDO:777`)
- [x] All references and IDs verified against `mondo-edit.obo`
- [x] Definitions match the corrected wording from @LengUNC's follow-up comment
- [x] Existing parents of reparented children left intact
- [x] term_tracker_item points to the originating issue
- [x] Curator note about atrioventricular block respected

---
🤖 **Generated by claude agent**
- Runtime: `claude`
- Model: `claude-opus-4-7`
- Agent config: `ai4curation/mondo-agent-config@v3:.`
- Iteration: `1`
- Run: [View workflow run](https://github.com/ai4curation/eval-ont-agent-mondo/actions/runs/25819422715)
