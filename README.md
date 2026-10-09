# Serum metabolites and postpartum depression

Download `PPD_MR_reproducibility_20261008.zip` and extract it. The archive contains 87 files with analysis scripts, SNP-level summary association data, archived outputs and supplementary tables. Run the commands below from the extracted `ppd-metabolite-mr` directory.

# Supplementary analysis materials

Run commands from this directory. Original primary MR estimates are supplied unchanged; primary result tables remain separate from supplemental reproduction and diagnostic scripts.

## FDR
Run `Rscript R/01_fdr.R`. This uses fdrtool 1.2.18 on 485 original primary P values and 30 reported MVMR P values. One of 486 planned primary estimates is unavailable. The original MVMR P values have limited printed precision.

## Strict exposure threshold
Run `Rscript R/02_strict_threshold.R <M01573.metal.pos.txt.gz>` against the source guanosine GWAS. The complete GWAS is not bundled. Its MD5 and verified count are supplied in support: 2,545,642 rows; zero P<5e-8; minimum P=8.815e-7 at rs16887484. No MR or clumping is performed by this script.

## Colocalization
Twelve regional input tables and 108 task definitions are supplied in coloc. Run `Rscript R/03_coloc_task.R 1` for task 1; use each unique task_id from coloc/tasks.tsv for the remaining tasks. R packages: data.table, jsonlite, coloc 5.2.3. Outputs are written to coloc/tasks. The original reference outputs are separate in coloc/reference_output. These regional revision analyses do not change the original 12-instrument MR estimate. Per-task settings describe priors, windows and exposure variance assumptions.

## Functional annotation and phenotype searches
support/VEP_raw contains all 12 archived VEP responses, with all returned consequence records tabulated separately. Multiple genomic placements are retained. Data release 116 was reported by the queried GRCh37 service; this does not establish a separately recorded VEP executable version.

The LD and Catalog tables cover 189 unique lead/proxy variants (EUR r2>=0.8 within 500 kb). Five association records met P<5e-8. The per-variant coverage table was reconstructed from the archived search output, including zero-hit variants; it is not an original HTTP request log. The search covered the GWAS Catalog curated published associations release of 13 September 2026, retrieved 5 October 2026. It is not an exhaustive phenome scan. PhenoScanner was unavailable.

`python annotate_guanosine.py --references <reference-directory> --eur-prefix <EUR-PLINK-prefix> --plink <PLINK-executable>` reproduces the available annotation workflow. The reference directory must contain Ensembl/*.json and GWAS_Catalog/associations.zip from the stated releases. Archived VEP responses are bundled; the full Catalog download and EUR genotype reference are not. See https://www.ebi.ac.uk/gwas/docs/file-downloads/ and https://grch37.rest.ensembl.org/ . Supply the archived versions to avoid changes from a later database release.

## Robust estimators and reverse MR
Original D-IVW and MR-RAPS numerical estimates are retained in the result tables. Their exact original runtime versions and complete settings have not been verified; no subsequently recovered candidate function is represented as the proven original implementation.

Reverse MR has one instrument and is reported as a Wald ratio on the continuous guanosine scale. The original beta, SE and P are unchanged. Multi-instrument heterogeneity and sensitivity tests are not estimable.

The selected current robust-method environment is R 4.3.3, MendelianRandomization 0.10.0 and mr.raps 0.2. See ROBUST_ENVIRONMENT.md for defaults and the distinction from unverified historical runtime versions.

Supplementary pathway analysis: see pathways/README.md for complete inputs, all tested pathways, contributors and FDR reproduction. This is a separate 2026-library analysis, reported separately from the original web analysis.

## Multivariable MR
Historical code/output and supplementary diagnostic results are supplied in MVMR.

## Joint MVMR input and diagnostic scripts
See MVMR/README.md for the reconstructed 977-row input, 30-exposure covariance approximation, archived output and runnable diagnostic/deduplication scripts. See robust_estimators/README.md for recovered D-IVW/MR-RAPS source materials and the remaining historical-runtime uncertainty.
