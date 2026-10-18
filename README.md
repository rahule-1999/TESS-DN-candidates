# Dwarf Nova Candidates in TESS

This repository contains a table of **144 photometrically selected dwarf nova (DN) candidates** studied using TESS light curves of sources reported to the Transient Name Server (TNS).

The table accompanies an AAVSO presentation by **Rahul Ethirajulu, Texas Tech University**. It provides source identifiers, sky positions, historical reported magnitudes and TESS observing metadata for exploring the sample. The DN identifications are provisional and require further supporting evidence, particularly spectroscopy.

## File

**`DN_candidates_details.csv`** contains 144 rows, one per unique source, and 10 columns. It is a metadata table, rather than a collection of light curves or spectra.

## Column descriptions

| Column | Description | Units / format |
| --- | --- | --- |
| `name` | TNS source identifier, without the AT or SN prefix, as retained in the source catalogue. | Text, e.g. `2018eny` |
| `sector` | TESS sector associated with the analysed light curve. It does not list every sector in which the source may have been observed. | Integer; blank if unavailable |
| `ra` | Catalogue right ascension. | Decimal degrees, 0 to 360 |
| `dec` | Catalogue declination. | Decimal degrees, -90 to +90 |
| `mag` | Historical reported magnitude retained from the transient catalogue. This is not necessarily the outburst peak, a quiescent magnitude or a TESS-band magnitude. | Apparent magnitude |
| `disc_tjd` | Reported discovery epoch expressed using the TESS Julian Date offset, `TJD = JD - 2457000`. | Days |
| `type` | Classification label retained from the source catalogue, rather than a new DN subtype assigned by this study. | Text |
| `group` | Reporting/discovery group label retained from the source catalogue. Multiple labels may occur in one quoted CSV field. | Text |
| `cam` | TESS camera associated with the analysed observation. | Integer, 1-4; blank if unavailable |
| `ccd` | CCD within the listed TESS camera. | Integer, 1-4; blank if unavailable |

The discovery timestamp alone does not establish that TESS captured the discovery or the same outburst. The timestamp convention above specifies the numerical offset; this CSV does not independently document the time standard or a barycentric correction for `disc_tjd`.

## Classification labels

The current CSV retains the following catalogue labels:

| `type` | Number of sources |
| --- | ---: |
| `Unclassified` | 123 |
| `CV` | 19 |
| `PSN` | 1 |
| `Nova` | 1 |
| **Total** | **144** |

`CV` means cataclysmic variable and `PSN` means possible supernova. These are inherited catalogue labels and may differ from interpretations suggested by the TESS light curves or from classifications added to TNS later. Their presence does not confirm or exclude a DN interpretation for an individual source.

## Interpreting the magnitudes and observing prospects

- The `mag` values describe historical reported brightness. They do not establish how bright a source is today or in quiescence.
- This CSV does not include the magnitude filter or its uncertainty. Check the original report before comparing measurements from different surveys or planning an observation.
- Most candidates lack secure quiescent magnitudes, limiting outburst-amplitude estimates and tests of relations reported in the literature.
- TESS single-band light curves alone do not provide color evolution during outburst.
- Spectra would help establish CV identity and composition. Subtype classification also uses light-curve behaviour.

Some candidates may be accessible to 12-20 inch telescopes during outburst. Feasibility depends on current brightness, equipment, sky conditions and the measurement required. Quiescent imaging and spectroscopy require separate assessments.

This table is a research resource. It does not constitute an organised observing campaign or provide a coordinated reporting channel.

## Looking up a source

Use the source name or coordinates on the [TNS search page](https://www.wis-tns.org/search). An individual source page has the form:

```text
https://www.wis-tns.org/object/2018eny
```

Check the source record for available classification reports, photometry, filters and spectra. This CSV is a snapshot and does not automatically update from TNS.

## Reading the table in Python

```python
import pandas as pd

data = pd.read_csv("DN_candidates_details.csv")
print(data.head())
```

Empty cells indicate unavailable metadata. One source has blank `sector`, `cam` and `ccd` fields. All 144 rows have names, coordinates, magnitudes, discovery epochs, type labels and group labels.

## Data provenance and references

The CSV contains selected metadata columns copied without changing their values from the research analysis results. The analysis pipeline obtains these metadata from the MIT TESS transient catalogue. The selection of 144 DN candidates is part of the presenter's research, rather than an official TNS classification list.

- [MIT TESS transient catalogue](https://tess.mit.edu/public/tesstransients/lc_bulk/count_transients.txt)
- [MIT TESS Transients documentation](https://tess.mit.edu/public/tesstransients/pages/readme.html)
- [Transient Name Server](https://www.wis-tns.org/)

When discussing or using individual objects, acknowledge the original discovery and classification reports as appropriate, alongside the research that identified this candidate sample.
