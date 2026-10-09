# WP lab

Two notebooks covering lineage tracing and literature collection. Both include their code, outputs and brief explanations.

## Run

Use Python 3.10:

```bash
python3.10 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m jupyter nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=600 task1_lineage.ipynb
python -m jupyter nbconvert --to notebook --execute --inplace task2_literature.ipynb
```

You can also open the notebooks in Jupyter or VS Code and run all cells with the environment's Python kernel.

Task 1 downloads about 333 MB on its first run. Set `DARLIN_DATA` to an existing H5AD file to skip the download. Task 2 runs offline using `inputs/`. Its `ONLINE` and `REFRESH` settings enable full-text downloads and a new search. A changed search requires updated screening decisions.

## Task 1

Reproduces two analyses from the [CoSpar DARLIN tutorial](https://cospar.readthedocs.io/en/latest/20231122_DARLIN_in_vivo_hematopoiesis.html): clone output and clonal coupling.

Of 140 HSPC-associated clones with selected downstream output, 68 (48.6%) have one observed outcome. HSC–MkP coupling is 0.381, with BH-adjusted q ≈ 0.00150 from 10,000 permutations. Sparse sampling limits conclusions about lineage restriction. The dataset has one collection time; the tutorial's `t0/t1` labels group cell types rather than establish observed transitions.

## Task 2

Collects 25 papers on endothelial cell identity using the [reference workflow](https://pmc.ncbi.nlm.nih.gov/articles/PMC12667862/#S8). The October 5 search found 166 records; the first 60 supplied the selected sample. SQLite stores metadata and TF-IDF supports search. The initial run retrieved 17 full texts. Annotations use abstracts and need human review.

`inputs/` contains source records, screening decisions, annotations and download history. `results/` contains the two figures and paper table. Further outputs are generated when the notebooks run.

## Problems encountered

Python 3.10 and pinned packages resolved dependency conflicts. The DARLIN server returned 403, so the alternate tutorial link supplied the data. Semantic Scholar returned 429; PubMed worked. Missing cell labels count toward clone size but stay out of selected-fate analysis. PMC's retired download endpoint required switching to its current OAI-PMH API.
