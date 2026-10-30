# OTCGEN: Open TIMES City, Generative

OTCGEN is an open energy-system model of a single city, for the IEA-ETSAP
TIMES model generator. It is built to be adapted to any city: the city
itself is one region, and the eGRID subregion that supplies its
electricity is a second. As released by the US EPA, and so at its
starting point here, it is populated with data for New York City. It is
developed and maintained by Energy Systems Modelling Analytics Ltd (ESMA),
Galway, Ireland, and published under an open licence (CC BY-SA 4.0).

> **Status: under redevelopment.** This repository holds the Veda model
> of the US EPA's Generative COMET v0.0.0 as released (tag
> `gcomet-v0.0.0`) and the GAMS-ready export of its reference scenario,
> GC_REF (`dd/`). ESMA's redevelopment follows as later commits.

## Not a US EPA model

OTCGEN is **not developed by, maintained by, reviewed by or endorsed by the
United States Environmental Protection Agency (US EPA).** It is an
independent redevelopment by ESMA.

The US EPA's **Generative COMET** (Generative City-based Optimization Model
for Energy Technologies) is the starting point for that redevelopment.
Everything published in this repository after that starting point is
ESMA's work, and the US EPA bears no responsibility for it. Results
produced with OTCGEN are not US EPA results and should not be presented or
cited as such. Nothing in this repository uses the US EPA's name, seal or
logo to suggest endorsement.

## Lineage and provenance

| | |
| --- | --- |
| Starting point | Generative COMET, the generic, city-scale version of the US EPA's COMET model for the TIMES model generator, developed for the EPA Office of Research and Development (ORD) |
| Generative COMET version | v0.0.0, published by EPA ORD on data.gov ([DOI 10.23719/1532263](https://doi.org/10.23719/1532263)); the archive's SHA-256 is recorded with its import |
| Status of the starting point | US EPA data are in the US public domain by default, "unless otherwise specified" ([EPA data licence](https://pasteur.epa.gov/license/sciencehub-license.html)) |
| Redevelopment | ESMA Ltd, from 2026 |

Generative COMET is documented in Kaplan, O., K. Vaillancourt, M. Pied,
R. Chaffanjon, F. Pedroli, D. Cooley and N. Dietsch (2025), *Generative
City-based Optimization Model for Energy Technologies: COMET Documentation
and User Guide*, US EPA, EPA/600/B-25/077
([DOI 10.23719/1532263](https://doi.org/10.23719/1532263)). The guide
records that the technical work was performed by Abt Global and its
sub-contractor, ESMIA Consultants.

How provenance is kept in this repository:

1. **The original first.** The first model commit holds the Generative
   COMET files exactly as released by the US EPA, unchanged. The commit
   message names the release and gives the SHA-256 checksum of the source
   archive, and the commit is tagged `gcomet-v0.0.0`. The import holds the
   Veda model (the release's folder `COMET_Generative_NYC/`) and leaves out
   two folders that Veda does not read to build the model: `Working_files/`
   (1.4 GB: the raw public data and generator workbooks for building a
   city's model, with copies for New York City and Chicago; one file is
   larger than GitHub's 100 MB limit) and `Exported_files/` (50 MB of
   results). They stay in the EPA archive; the import commit lists their
   names, sizes and SHA-256 checksums. Workbook properties and external
   links are as the US EPA released them.
2. **ESMA's changes after it.** Every change ESMA makes follows as later
   commits, so `git diff gcomet-v0.0.0` shows exactly how OTCGEN differs
   from the US EPA's original.
3. **GAMS-ready files with their origin.** Files exported from the Veda
   workbooks for GAMS are kept in `dd/<scenario>/`. `dd/README.md` records
   how each export was made: the source commit, the Veda version, the TIMES
   version targeted and the date.

## Licence

OTCGEN as distributed here, and ESMA's contributions to it, are licensed
under the Creative Commons Attribution-ShareAlike 4.0 International licence
([`LICENSE`](LICENSE), [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)).
Material that originates from the US EPA remains in the US public domain;
this licence does not restrict any use of public-domain material that the
law allows.

When you use or adapt OTCGEN:

- credit "OTCGEN, Energy Systems Modelling Analytics Ltd (ESMA)" and the
  original Generative COMET model by the US EPA Office of Research and
  Development;
- link to the CC BY-SA 4.0 licence and say whether you made changes;
- share your adaptations under the same licence (ShareAlike).

OTCGEN is provided as is, without warranties of any kind (section 5 of the
licence).

## Running the model

OTCGEN runs with the IEA-ETSAP TIMES model generator
([etsap-TIMES/TIMES_model](https://github.com/etsap-TIMES/TIMES_model),
GPL-3.0-or-later) under GAMS and an LP solver. The Veda workbooks can be
edited with Veda; the GAMS-ready files in `dd/` need only TIMES and GAMS.

OTCGEN is also one of the test models for TIMES.jl
([esma-ie/TIMESjl](https://github.com/esma-ie/TIMESjl)), an open
translation of TIMES to Julia/JuMP that is developed and tested only on
openly licensed models.
