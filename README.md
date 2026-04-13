# rac-us-nc

North Carolina jurisdiction-specific RAC source and encoding corpus.

This repo is for North Carolina-administered policy layers. Federal program
cores stay in `rac-us`; North Carolina overlays, manuals, guidance, and
state-specific encodings live here.

## Current scope

- NCDHHS FNS 360 source slices for North Carolina SNAP utility allowances
- NCDHHS FNS 340 source slices for North Carolina SNAP child-support deduction treatment
- jurisdiction-local source corpus for North Carolina SNAP overlays

## Layout

```text
rac-us-nc/
├── sources/
│   └── slices/
│       └── ncdhhs/
│           └── fns/
│               └── 360/
│                   └── current-effective/
├── scripts/
│   ├── check_no_promoted_stubs.py
│   └── validate_repo.py
└── CLAUDE.md
```

## Local commands

```bash
cd /Users/maxghenis/TheAxiomFoundation/rac
uv run python -m rac.validate all /Users/maxghenis/TheAxiomFoundation/rac-us-nc
uv run python -m rac.test_runner /Users/maxghenis/TheAxiomFoundation/rac-us-nc -v

cd /Users/maxghenis/TheAxiomFoundation/rac-us-nc
python3 scripts/validate_repo.py
```

## Encoding policy

- Repo boundaries follow jurisdictions.
- Keep North Carolina-administered overlays in `rac-us-nc`, even when they sit
  on top of a federal program like SNAP.
- Keep exact local excerpts in `sources/slices/`.
- When a North Carolina source sets a value inside a federally delegated slot,
  add a `*.meta.yaml` sidecar next to the source slice with `relation: sets`
  pointing to the canonical upstream CFR or USC target.
- Do not hand-edit promoted policy outputs; use AutoRAC plus benchmarked repair
  loops.
