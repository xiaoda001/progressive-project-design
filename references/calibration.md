# Calibration workflow

Run this when a slice is complete or documentation drift is discovered.

1. Compare the roadmap, L1 module documents, verification evidence, tests, configuration, and actual code.
2. Register implemented but undocumented interfaces before marking them D4.
3. Update `path#line` code locations and module backlinks.
4. Record overturned decisions and the reason for the change.
5. Promote affected modules from D3 to D4 only when behavior and evidence align.
6. Archive a slice retrospective beside its logs.

Calibration aligns existing scope. It does not add the next slice or expand requirements.
