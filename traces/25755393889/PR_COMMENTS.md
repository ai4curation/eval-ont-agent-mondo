## Summary
Relabeled `MONDO:0012277` from "myofibrillar myopathy 4" to "LDB3-related myofibrillar myopathy" as requested.

## Rationale
The request came from the ClinGen Muscular Dystrophies and Myopathies GCEP to use explicit gene-related names instead of numerical suffixes for myofibrillar myopathies.

## Changes
- Updated `name` to `LDB3-related myofibrillar myopathy`.
- Moved the previous name "myofibrillar myopathy 4" to a synonym with proper citations `[OMIM:609452, Orphanet:98912]`.
- Added citations to existing synonyms `MFM4`, `myofibrillar myopathy (disease) caused by mutation in LDB3`, `myofibrillar myopathy type 4`, `myopathy, myofibrillar, 4`, and `myopathy, myofibrillar, type 4` using `[OMIM:609452]`.
- Added `term_tracker_item` with the issue URL.

## Validation
- Verified that the new name "LDB3-related myofibrillar myopathy" did not already exist in the ontology.
- Normalized the OBO file using `run.sh make NORM`.
