# Impact of repeat test-takers on difficulty estimates from online vocabulary testing platforms

Code and data for the paper presented at JALT Vocab-SIG 2026 Symposium at Kyushu Sangyo 
University, 26 Sep 2026, Fukuoka, Japan.

Open, large-scale vocabulary testing platforms tend to produce very sparse response
matrices in which a minority of test-takers contribute a disproportionate share
of observations. This repository contains the preprocessing pipeline for those
human observations from an online testing platform, a simulation study with known 
parameters under comparable sparsity and repeat-testing conditions, and the resulting
difficulty estimates for 2,999 flemmas.

**Findings:** <one or two sentences — direction and magnitude of the
bias introduced by repeat test-takers, e.g. "difficulty estimates for
high-frequency items were displaced by a mean of X logits (SD = Y) when repeat
test-takers made up ~30% of observations.">

A mirror of this repository and the resulting wordlist is archived at
[OSF](https://doi.org/<osf-doi>).

## Contents

```
├── 01_preprocessing/    # raw platform exports → analysis-ready .csv
├── 02_simulation/       # sparse-matrix simulation with known parameters
├── 03_estimation/       # bigIRT calibration
└── 04_wordlist/         # 2,999 flemmas with difficulty estimates (.xlsx)
```

## Requirements

- R >= <version>
- CRAN packages: <list>
- [bigIRT](https://github.com/cdriveraus/bigIRT) (Driver & Tomasik, 2023),
  which is not on CRAN:

```r
  remotes::install_github("cdriveraus/bigIRT")
```

Exact package versions are pinned in `renv.lock`; run `renv::restore()` to
reproduce the environment.

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

Run: `01_preprocessing/<filename>.Rmd`

For transparency, the implementation details is viewable in .Rmd.

## 2. Simulation with repeat test-takers

Simulates a response matrix with known item and person parameters at 99% missingness, 
with repeat test-takers contributing approximately 30% of all observations. 
The dichotomous observations were drawn from a probability matrix 
described by the 1-IRT (or Rasch) model
P(X_{ni} = 1 \mid \theta_n, \beta_i) = \frac{\exp(\theta_n - \beta_i)}{1 + \exp(\theta_n - \beta_i)}
The seed is set at the top of the script (`set.seed(<n>)`);
results are reproducible without re-running the human-data pipeline.

Run: `02_simulation/<filename>.Rmd`

## 3. Estimating difficulty with bigIRT

Difficulty was estimated with a <1PL/Rasch | 2PL> model fitted in bigIRT.
Because the <Rasch difficulty scale is identified only up to an additive
constant | 2PL scale is identified only up to a location and scale
transformation>, estimates are anchored by <constraint, e.g. fixing mean item
difficulty to 0>. **Higher logits indicate greater difficulty.**

Run: `03_estimation/<filename>.Rmd`

## 4. Flemma list with Japanese EFL difficulty indices

Difficulty estimates for 2,999 flemmas for L1 Japanese EFL learners. A *flemma*
groups a lemma with its inflected forms but not its derivational family, so
`walk / walks / walked / walking` is one unit while `walker` is separate.
Flemmas were derived from <source list/corpus>.

Available as `04_wordlist/<filename>.xlsx` and as a read-only
[Google Sheet](<view-only-link>).

Columns: <flemma | difficulty_logit | SE | n_responses | ...>

## Citation

```bibtex
@inproceedings{<key>,
  author    = {<authors>},
  title     = {Impact of repeat test-takers on difficulty estimates from
               online vocabulary testing platforms},
  booktitle = {<proceedings>},
  year      = {2026}
}
```

## License

Code: <MIT / GPL-3>. Data and wordlist: <CC BY 4.0>.

## Contact

<name> — <email>
