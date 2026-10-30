# OTCGEN: GAMS-ready files

`dd/<scenario>/` holds what the TIMES model generator needs to run a
scenario without Veda: `<scenario>.run`, the `*.dd` files it includes,
`cplex.opt` and `times2veda.vdd`. Nothing else from the Veda export is kept,
and nothing was edited by hand.

| | |
| --- | --- |
| Source workbooks | tag `gcomet-v0.0.0`: Generative COMET v0.0.0 as released by the US EPA, unchanged |
| Exported with | Veda2 v5.0.0.0 (DD export of the Veda case `GC_REF`) |
| Exported | 30 Oct 2026, by ESMA |
| TIMES version targeted | v4.9.7 ([etsap-TIMES/TIMES_model](https://github.com/etsap-TIMES/TIMES_model) @ `d9a6a25`) |
| Scenarios | `gc_ref`: GC_REF, the reference scenario of the EPA user guide (EPA/600/B-25/077) |
| Checksums | `manifest.json`: every file with its size and SHA-256 |

The files are byte-exact (`.gitattributes`: no line-ending conversion), so
the checksums in `manifest.json` hold on every platform. TIMES.jl's
reference harness pins this folder by the SHA-256 of `manifest.json`.
`manifest.json` is kept exactly as written at the import; its `from` and
`imported` fields record where the export was checked before it was added
here.

## Checks made before publication (30 Oct 2026)

- The Veda model the export was made from was a clone of this repository at
  tag `gcomet-v0.0.0`. Every workbook and model file in it was
  byte-identical to the tag (SHA-256 of all 134 tracked files); only Veda's
  own settings in `AppData/` (`Cases.json`, `Groups.json`, `Settings.json`,
  `FrontEndFormFormSettings.json`) differed, which Veda rewrites when cases
  are defined.
- Every file is complete (each `*.dd` ends its last block with `/;`, and
  `base.dd` holds the timeslice tree, `TS_GROUP` and `TS_MAP`).
- The case compiles and preprocesses under TIMES v4.9.7 @ `d9a6a25` (GAMS
  54.6.1, run up to the SOLVE statement): normal completion, no
  domain-violation records, and all TIMES quality checks passed.
- Not yet solved here. A GAMS/CPLEX reference run follows in TIMES.jl's
  reference suite ([esma-ie/TIMESjl](https://github.com/esma-ie/TIMESjl)).

The other scenarios of the EPA release (GC_REF_nocons, GC_REF_SUB,
GC_REF_ZEV, GC_TAX, GC_NZ) were exported and checked in the same way on
30 Oct 2026 and can be added to `dd/` later.

## Running a scenario

With GAMS and the TIMES source (v4.9.7) on the include path, from
`dd/<scenario>/`:

    gams <scenario>.run idir1=<path to TIMES_model> lp=cplex

The run file uses REDUCE YES, as Veda wrote it. Any LP solver GAMS offers
can replace CPLEX.
