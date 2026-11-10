# Task: Eed-null versus E14 WT day-5 Hallmark GSEA

Using the supplied gene-expression matrix and mouse Hallmark GMT file, identify the top positively enriched Hallmark gene set in Eed-null cells relative to E14 wild-type cells at day 5. Use `ST106_Eed-d5_RNA_FPKM` as the Eed-null sample and `ST102_E14d5_RNA_FPKM` as the E14 WT sample.

Retain rows with FPKM ≥ 1.0 in at least one selected sample, applying this filter before resolving duplicate gene symbols. For each duplicated symbol, retain the Ensembl `gene_id` with the highest mean FPKM across the two selected samples; break exact mean-expression ties using the lexicographically smallest Ensembl ID.

Rank retained genes using `log2((Eed-null FPKM + 1) / (E14 WT FPKM + 1))`, in descending order. For exact ranking-score ties, order gene symbols alphabetically in ascending order; do not modify the scores or add jitter.

Run `gseapy.prerank` using the supplied mouse Hallmark GMT, `min_size=15`, `max_size=500`, `permutation_num=1000`, `weight=1`, `seed=0`, and `threads=1`. A gene set qualifies when NES > 0 and FDR q-value < 0.05. Select the qualifying gene set with the highest NES; if NES values are exactly tied, choose the gene-set name that sorts first alphabetically.

Save `output/answer.json` with exactly two keys: `top_gene_set` (the exact GMT term) and `nes` (rounded to three decimal places). Also save `output/answer.md` with the analysis summary and `output/analysis.py` containing the executable analysis. Report the number of ranked genes, tested gene sets, qualifying positive gene sets, and GSEApy version. Do not infer causality from this descriptive comparison.
