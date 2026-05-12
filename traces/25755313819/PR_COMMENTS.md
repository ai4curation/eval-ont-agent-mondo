## Summary
Updated the Orphanet cross-reference for MONDO:0009106 (diastematomyelia).

## Changes
- Changed `xref: Orphanet:1671` to `xref: Orphanet:573278`
- Updated `subset` sources from `Orphanet:1671` to `Orphanet:573278`
- Updated `synonym` citations from `Orphanet:1671` to `Orphanet:573278`
- Updated source attribution in other `xref` entries (ICD10CM, MedDRA, OMIM) from `Orphanet:1671` to `Orphanet:573278`

## Rationale
The issue reported that Orphanet:1671 (Split cord malformation type I) was too narrow for the concept of diastematomyelia and recommended using Orphanet:573278 (Split cord malformation) instead. This aligns with SNOMED CT, where split cord malformation and diastematomyelia are considered synonyms.

## Validation
- Verified current term content using `obo-grep.pl`.
- Performed edits on the checked-out term file `terms/MONDO_0009106.obo`.
- Checked back the changes using `obo-checkin.pl`.
