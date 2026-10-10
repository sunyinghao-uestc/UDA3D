# UDA3D

This repository provides the literature-search records and method-level
metadata accompanying the survey:

> **Unsupervised Domain Adaptation for 3D Object Detection: A Survey**

The repository documents the evidence pipeline used to construct the
survey corpus. It contains the database-specific queries, original
database exports, merged and deduplicated search results, and the final
evidence matrix used to generate the survey statistics and supplementary
method tables.

## Corpus at a Glance

- **Search period:** 2020 through September 2026
- **Search date:** September 2026
- **Search fields:** publication titles
- **Databases searched:** OpenAlex, arXiv, IEEE Xplore, Scopus, and Web of Science
- **Raw database records:** 1,159
- **Unique records after deduplication:** 666
- **Methods identified from database records:** 59
- **Methods added through citation chasing:** 5
- **Final in-scope method entries:** 64
- **Modalities covered:** LiDAR, camera, and multimodal perception
- **UDA settings covered:** standard, source-free, multi-source, and multi-target offline UDA

The 64 entries are method-level records rather than a simple count of
publication files. When a preprint and a subsequent archival publication
describe the same method, they are represented as one method entry.

## Corpus Construction

The corpus was constructed in four stages:

1. **Database search.** Two groups of title terms were combined. The
   first described 3D detection and perception, including LiDAR, point
   cloud, and bird's-eye-view terms. The second described cross-domain
   learning, including domain adaptation, domain shift, source-free, and
   sim-to-real terms. Terms for adjacent settings were retained during
   retrieval so that eligibility could be determined from the paper rather
   than its title alone.
2. **Deduplication.** Titles were normalized for case, Unicode and
   typographic variants, punctuation, and spacing. Records with the same
   normalized title were merged, reducing 1,159 raw records to 666 unique
   records.
3. **Eligibility screening.** All 666 unique records underwent title and
   available abstract screening. Full texts of potentially eligible studies
   were then assessed against the survey's problem-setting and application
   scope.
4. **Citation chasing.** Backward and forward citation searches added five
   eligible methods missed by the title queries: SN, 3D CoCo, Rote-DA,
   PR-BEV+, and GA-RP3D. The final corpus contains 64 method entries, of
   which 59 were identified from the database records and five through
   citation chasing.

```text
database queries -> 1,159 raw records -> 666 unique records
                 -> eligibility screening -> citation chasing -> 64 methods
```

## Search Sources

The searches combine title terms related to 3D detection and perception
with terms related to domain adaptation, cross-domain transfer, domain
shift, and related settings. The same conceptual logic was adapted to the
syntax and query limits of each database. The files linked below contain
the exact query specifications used for retrieval.

| Database | Raw records | Query | Original export |
|---|---:|---|---|
| OpenAlex | 760 | [Query](queries/openalex/query.md) | [Export](raw_data/openalex/results.xlsx) |
| arXiv | 143 | [Query](queries/arxiv/query.md) | [Export](raw_data/arxiv/results.xlsx) |
| IEEE Xplore | 77 | [Query](queries/ieeexplore/query.md) | [Export](raw_data/ieeexplore/results.xlsx) |
| Scopus | 147 | [Query](queries/scopus/query.md) | [Export](raw_data/scopus/results.xlsx) |
| Web of Science | 32 | [Query](queries/wos/query.md) | [Export](raw_data/wos/results.xlsx) |
| **Total** | **1,159** |  |  |

The database exports retain their original, database-specific fields and
formats. Consequently, the available bibliographic fields are not uniform
across the five sources.

## Survey Scope

The corpus focuses on offline unsupervised domain adaptation for outdoor
3D object detection in autonomous driving and related robotic perception
settings.

### Included settings

- Standard UDA using labeled source data and unlabeled target data
- Source-free UDA using a source-trained detector and unlabeled target data
- Multi-source UDA
- Multi-target UDA
- LiDAR-based, camera-based, and multimodal 3D object detection
- Conference, journal, workshop, and preprint studies satisfying the
  eligibility criteria

### Excluded settings

Studies devoted exclusively to the following settings are not included
in the 64-method UDA corpus:

- Test-time or online adaptation
- Domain generalization
- Semi-supervised domain adaptation
- Active domain adaptation
- Multi-dataset supervised training
- Corruption benchmarking without target-domain adaptation
- Indoor 3D detection or tasks other than 3D object detection

Related studies from these adjacent settings may be discussed in the
survey to clarify the task boundary, but they are not included in the
method statistics or quantitative UDA comparisons.

## Repository Structure

```text
UDA3D/
├── README.md
├── LICENSE
├── queries/
│   ├── arxiv/query.md
│   ├── ieeexplore/query.md
│   ├── openalex/query.md
│   ├── scopus/query.md
│   └── wos/query.md
├── raw_data/
│   ├── arxiv/results.xlsx
│   ├── ieeexplore/results.xlsx
│   ├── openalex/results.xlsx
│   ├── scopus/results.xlsx
│   └── wos/results.xlsx
├── deduplicated/
│   └── results.xlsx
└── metadata/
    └── evidence_matrix.xlsx
```

### `queries/`

Contains the database-specific search expressions used for retrieval.
The wording follows the same conceptual search logic but is adapted to
the search syntax of each database.

### `raw_data/`

Contains the original exports obtained from the five databases. These
files preserve the database-specific fields and have not been converted
to a common schema.

### `deduplicated/results.xlsx`

Contains the 666 unique bibliographic records obtained after merging and
deduplicating the five database exports. Each row is assigned a stable
record identifier of the form `DSR-XXXX`.

The workbook records:

- representative title;
- contributing databases;
- number of matched raw records;
- publication year;
- authors;
- venue or subject category;
- DOI; and
- URL.

### `metadata/evidence_matrix.xlsx`

Contains the final 64-entry method-level corpus used to generate the
survey statistics and supplementary method tables. The workbook contains
one worksheet, `metadata`, with 64 data rows and 25 fields.

The recorded attributes include:

- method name and publication information;
- UDA setting;
- training and inference modalities;
- primary and secondary adaptation signals;
- adaptation loci;
- transfer or test contexts and recorded datasets;
- baseline detectors, evaluated categories, and evaluation protocols;
- evaluated domain-shift categories; and
- code availability and repository URLs.

## Current Corpus Summary

The following counts are calculated from
[`metadata/evidence_matrix.xlsx`](metadata/evidence_matrix.xlsx). Counts
for signals, loci, and domain shifts are non-exclusive because the taxonomy
is multi-label.

### Problem settings

| Setting | Methods |
|---|---:|
| Standard UDA | 54 |
| Source-free UDA | 5 |
| Source-free multi-source UDA | 2 |
| Multi-source UDA | 1 |
| Multi-target UDA | 2 |

### Adaptation signals and loci

| Adaptation signal | Methods | Adaptation locus | Methods |
|---|---:|---|---:|
| S1: Prior-guided distribution shaping | 28 | L1: Input and scene space | 39 |
| S2: Inter-domain distribution alignment | 22 | L2: Feature and representation space | 31 |
| S3: Target pseudo-supervision | 50 | L3: Object-centric representation and proposal space | 21 |
| S4: Paired consistency regularization | 32 | L4: Prediction output and target-supervision space | 51 |
| S5: Auxiliary and privileged supervision | 15 | L5: Model and optimization space | 35 |

### Evaluated domain shifts

| Domain-shift category | Methods | Percentage of corpus |
|---|---:|---:|
| LiDAR beams | 48 | 75.0% |
| Geography | 47 | 73.4% |
| Weather | 12 | 18.8% |
| Sim-to-real | 8 | 12.5% |
| Illumination | 7 | 10.9% |
| Camera configuration | 4 | 6.3% |
| Viewpoints | 3 | 4.7% |
| LiDAR mechanisms | 2 | 3.1% |

Code is available for 25 of the 64 method entries (39.1%).

## Taxonomy Metadata

The method-level metadata follows the survey's multi-label
**Adaptation Signal × Adaptation Locus** taxonomy.

### Adaptation signals

- **S1:** Prior-guided distribution shaping
- **S2:** Inter-domain distribution alignment
- **S3:** Target pseudo-supervision
- **S4:** Paired consistency regularization
- **S5:** Auxiliary and privileged supervision

### Adaptation loci

- **L1:** Input and scene space
- **L2:** Feature and representation space
- **L3:** Object-centric representation and proposal space
- **L4:** Prediction output and target-supervision space
- **L5:** Model and optimization space

A method may receive multiple signal and locus codes when it contains
separate adaptation components.

## Citation

If you use this corpus, taxonomy, or evidence matrix, please cite the
accompanying survey:

> *Unsupervised Domain Adaptation for 3D Object Detection: A Survey.*

Complete bibliographic information will be added after publication.
