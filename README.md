# Impact of repeat test-takers on difficulty estimates from online vocabulary testing platforms

<i>Code and data for the paper presented at JALT Vocab-SIG 2026 Symposium at Kyushu Sangyo 
University, 26 Sep 2026, Fukuoka, Japan.</i>

Open, large-scale vocabulary testing platforms tend to produce very sparse response
matrices in which a minority of test-takers contribute a disproportionate share
of observations. This repository contains the preprocessing pipeline for those
human observations from an online testing platform, a simulation study with known 
parameters under comparable sparsity and repeat-testing conditions, and the resulting
difficulty estimates for 2,999 flemmas.

**Findings:** The results suggest that 1-IRT-modeling using a combination of JLM and 
Bayesian estimation from the package bigIRT (version 0.1.8) (Driver & Tomasik, 2023) 
produces item estimates that might be robust to repeat test-takers. Thus, a ranked flemma-based 
wordlist for Japanese EFL learners using large-scale observations extracted from an online 
vocabulary testing platform  [vlt.carleton.ca](https://vlt.carleton.ca/) (McLean & Raine, 2019) 
is presented here.

A copy of this repository and the resulting wordlist is also archived at
[OSF](https://doi.org/<osf-doi>).

## Contents

```
├── appendix_a-preprocessing.Rmd/    # raw platform exports → analysis-ready .csv
├── appendix_b-demo.Rmd/             # sparse-matrix simulation with known parameters
├── appendix_c-irt.Rmd/              # bigIRT calibration
└── appendix_d-flemmas.xls/          # 2,999 flemmas with difficulty estimates (.xlsx)
```

## Requirements

- R >= 4.6.1
- Rtools45
- CRAN packages: dplyr, ggplot2, reshape2, rmarkdown, stringi, igraph, data.table
- [bigIRT](https://github.com/cdriveraus/bigIRT) (Driver & Tomasik, 2023),
  which is not on CRAN:

```r
  remotes::install_github("cdriveraus/bigIRT")
```

## 1. Data preprocessing

Human observations were extracted from the response database of the vocabulary
testing platform at [vlt.carleton.ca](https://vlt.carleton.ca/). The initial 
dataset contained 1.3 million responses to 8149 test items and 45,965 logged 
sessions. Raw exports were filtered for invalid responses by removing 
responses (rows) that contained any non-Japanese script, items (columns) with 
response patterns that were either all “1”s or all “0”s, and responses (rows) 
with average reaction times that fell outside of the 3-to-14-second range. 
Unlinked items that form fragmented “islands” of observations that could lead to 
biased estimates were also removed prior to running bigIRT on the dataset.

For transparency and analytical integrity, implementation details are
viewable at [Appendix A](https://www.moonspacelinguistics.github.io/appendix_a-preprocessing.html)
(source code is available as `appendix_a-preprocessing.Rmd`).

## 2. Simulation with repeat test-takers

Three dataframes were simulated: 
- **DF**: the original dataframe with “test-takers” (noriginal = 4000) who
  answered all “items” (k = 2000)
- **DF_missing**: a copy of DF, except that each “test-taker” responded only to 20
  out of the 2000 “items”, which was created by randomly removing observations from DF.
  This creates a sparse dataset with 99% missing observations.
- **DF_repeat**: created by first duplicating DF_missing, and then have 10% of the
  “test-takers” chosen randomly for duplication between one and five times. This
  results in a dataframe that has altogether nrepeat = 5153 rows of responses, of
  which 1553 of the rows (making up 30.1% of the observations) were responses from
  the same 400 “individuals” who “retook the same test” for two to six times.

The dichotomous observations for DF were drawn from a probability matrix 
described by the 1-IRT (or Rasch) model

```math
P(X_{ni} = 1 \mid \theta_n, \beta_i) = \frac{\exp(\theta_n - \beta_i)}{1 + \exp(\theta_n - \beta_i)}
```

where person ability $`\theta_n`$ and item difficulty $`\beta_i`$ are drawn from
$`\mathcal{N}(0,1)`$. The seed is set at the top of the script (`set.seed(<n>)`);
results are reproducible without re-running the human-data pipeline.

For replicability, users can run the simulation `appendix_b-demo.Rmd`, and the knitted
RMarkdown file is viewable at [Appendix B](https://www.moonspacelinguistics.github.io/appendix_b-demo.html).

## 3. Estimating difficulty with bigIRT

Difficulty was estimated with a 1PL/Rasch model fitted in bigIRT.
Because the Rasch difficulty scale is identified only up to an additive
constant, estimates are anchored by fixing mean item
difficulty to 0. **Higher logits indicate greater difficulty.**

For transparency and analytical integrity, the implementation details are viewable 
at [Appendix C](https://www.moonspacelinguistics.github.io/appendix_c-irt.html)
(source code is available as `appendix_c-irt.Rmd`).

## 4. Flemma list with Japanese EFL difficulty indices

Difficulty estimates for 2,999 items for L1 Japanese EFL learners. A *flemma*
groups a lemma with its inflected forms but not its derivational family, so
`run / runs / ran / running` is one unit while `runner` is separate.
However, it should be noted that the current list contains duplicates due to the platform's 
backend processes, and users should take this into consideration when using the wordlist.

Available as `appendix_d-flemmas.xlsx` and as a read-only at
[Google Sheet](https://docs.google.com/spreadsheets/d/1ibqLGDiIHkmt2ExeN_PiwK7Nz-7cnMh2Hs3y2q6IxQQ/edit?gid=0#gid=0).

Columns: No. | Item ID | flemma | Estimate

## Citation

```bibtex
@inproceedings{tan2026repeat,
  author    = {Tan, Liang Ye and McLean, Stuart},
  title     = {Impact of repeat test-takers on difficulty estimates from
               online vocabulary testing platforms},
  booktitle = {Vocabulary Learning and Instruction},
  year      = {pending}
}
```

## License

Code: MIT. Data and wordlist: CC BY-NC-SA 4.0.

## Contact

Tan, Liang Ye
tun91232@temple.edu

