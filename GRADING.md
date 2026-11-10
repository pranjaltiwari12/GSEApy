# Grading rubric (100 points)

1. **Top term identity — 25 points.** Pass if `top_gene_set` is exactly `HALLMARK_EPITHELIAL_MESENCHYMAL_TRANSITION`; fail if another term or multiple terms are returned.
2. **NES value — 20 points.** Pass if `nes` is within 2.37–2.46 for the specified configuration. The observed seed-0 reference is 2.405; seed-sensitivity runs (0–4) ranged from 2.394 to 2.434. Fail outside the tolerance or if several NES values are supplied.
3. **Sample choice and direction — 15 points.** Pass if the model uses `ST106_Eed-d5_RNA_FPKM` as numerator/Eed-null and `ST102_E14d5_RNA_FPKM` as denominator/E14 WT; fail if other samples or reversed direction are used.
4. **Preprocessing and ranking — 15 points.** Pass if FPKM ≥1 in either selected sample is filtered before duplicate resolution; duplicate symbols retain highest mean FPKM with lexical Ensembl-ID tie-break; ranking uses the specified log2 ratio and exact-score tie ordering by symbol. Fail if processing order/rules differ or scores are jittered.
5. **GSEA configuration and significance — 15 points.** Pass if mouse Hallmark GMT, GSEApy 1.3.2, 1,000 permutations, `min_size=15`, `max_size=500`, `weight=1`, `seed=0`, `threads=1`, and qualification NES >0 plus FDR q-value <0.05 are used. Fail for `random_state`, human GMT, other settings, or omitted threshold.
6. **Required artifacts and reporting — 10 points.** Pass if `output/answer.json` contains exactly `top_gene_set` and `nes`, `output/answer.md` summarizes analysis, and `output/analysis.py` is executable from the repository root. The report should state ranked-gene, tested-set, qualifying-set counts and GSEApy version.

## Trap / common wrong approaches

- `GSE53506_RPKM_table.txt.gz` is the GEO file name, but the selected matrix columns are labelled FPKM. Use those selected columns and their labels.
- GSE53506 is the RNA-seq subseries; the article cites the parent super-series GSE53508 as the data-deposition accession.
- Do not use the pre-existing paper-level FPKM/RPKM values as a substitute for running the requested Hallmark GSEA.
- Do not use `random_state=0`: `gseapy.prerank` accepts `seed=0`.
- Do not claim ties are fully resolved inside GSEApy; its warning remains even with deterministic input ordering.

## Observed sensitivity values

Sezed 0: NES 2.405; seed 1: 2.427; seed 2: 2.394; seed 3: 2.434; seed 4: 2.401. All five runs selected the same top term and returned 26 qualifying positive sets. No validated numeric “wrong-method” answer is asserted; do not invent one.
