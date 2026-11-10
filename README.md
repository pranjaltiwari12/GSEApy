# GSEApy benchmark: Eed-null versus E14 WT day 5

## Run the reference solution

From the repository root:

```powershell
python -m pip install -r requirements.txt
python output/analysis.py
```

The reference script resolves `data/` relative to the repository root and writes all generated artifacts to `output/`. It requires GSEApy 1.3.2.

## Repository contents

- `TASK.md` — benchmark request
- `GRADING.md` — scoring criteria
- `requirements.txt` — Python dependencies
- `data/GSE53506_RPKM_table.txt.gz` — GEO processed expression matrix
- `data/mh.all.v2026.2.Mm.symbols.gmt` — mouse Hallmark gene sets
- `output/analysis.py` — executable reference solution
- `output/answer.json` and `output/answer.md` — golden outputs
- `output/ranked_genes.tsv`, `output/gsea_results.tsv`, `output/qualifying_positive_results.tsv` — analysis intermediates
- `output/seed_sensitivity_summary.tsv` — recorded seeds 0–4 sensitivity results

## Golden answer

```json
{
  "top_gene_set": "HALLMARK_EPITHELIAL_MESENCHYMAL_TRANSITION",
  "nes": 2.405
}
```

## Recorded seed sensitivity

Seeds 0–4 all returned the same leading gene set and 26 qualifying positive gene sets. The leading NES values were 2.405, 2.427, 2.394, 2.434, and 2.401, respectively (range 2.394–2.434). These are recorded from the earlier five-seed run; the single-seed reference script does not recompute them.

## Important reproducibility caveat

The ranked list contains 37 repeated ranking-score entries. The input is sorted by descending score and then ascending gene symbol for exact ties, with no score jitter. GSEApy still warns that tied statistics may be internally reordered. Do not describe the internal tie handling as guaranteed deterministic. GSEApy-reported zero p/FDR estimates are finite-permutation estimates, not literal probabilities of zero.

## Provenance and licensing

The expression file `GSE53506_RPKM_table.txt.gz` is the processed expression supplementary file for GEO subseries GSE53506, an RNA-seq subseries within super-series GSE53508. The associated PLOS ONE article identifies GSE53508 as the overall data-deposition accession. The selected sample columns are explicitly labelled FPKM in the matrix, notwithstanding `RPKM` in the filename.

Article: Thornton SR, Butty VL, Levine SS, Boyer LA. *Polycomb Repressive Complex 2 Regulates Lineage Fidelity during Embryonic Stem Cell Differentiation*. PLOS ONE. 2014;9(10):e110498. https://doi.org/10.1371/journal.pone.0110498. The PLOS article page states that the article is distributed under the Creative Commons Attribution License (CC BY); the article page links to the license. Cite the paper and attribute it when reusing article content.

MSigDB mouse release v2026.2.Mm exists (October 2026). MSigDB releases v2022.1 and later are generally under CC BY 4.0, with additional restrictions for certain legacy gene-set subsets (notably specified KEGG/BioCarta sets). This task uses the Mouse Hallmark collection, not those named legacy subsets. Retain MSigDB attribution and check the official license terms before redistribution or commercial reuse.

GSEApy 1.3.2 is used as the analysis package; retain its BSD-3-Clause license notice if redistributing the software.
