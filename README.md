# Chemistry-Informed Machine Learning and Multi-Objective Optimization of Alkali-Activated Concrete

Code and data for a study on chemistry-informed machine learning and multi-objective
optimization of fly ash and slag alkali-activated concrete (AAC).

**Authors**
Abolfazl Afshin ([ORCID 0000-0003-4861-3087](https://orcid.org/0000-0003-4861-3087))
Ali Behnood ([ORCID 0000-0003-2537-1863](https://orcid.org/0000-0003-2537-1863))

Department of Civil Engineering, University of Mississippi, Oxford, MS 38677, USA

> This work is currently under review. Citation details will be added once the paper is published.

---

## Overview

A chemistry-informed machine learning surrogate is trained to predict the compressive strength
of fly ash and slag alkali-activated concrete, and is then used inside a multi-objective
optimization to search for mixtures that balance strength against carbon emissions and material
cost under two curing scenarios.

Three elements distinguish the framework:

1. **Chemistry-informed inputs.** Oxide molar ratios are computed on a system basis, so binder
   chemistry enters the model directly rather than through raw mixture quantities alone.
2. **Conformal strength objective.** The optimizer maximizes a one-sided 90% conformal lower
   bound on strength rather than a point prediction, so each candidate mixture is credited only
   with the strength it can be expected to reach.
3. **Curing as a decision variable.** In the second scenario the optimizer chooses between
   ambient curing and a heat cycle, and pays for that choice in energy, carbon, and cost.

---

## Dataset

Dataset contains 2370 records covering 1226 unique
mixtures compiled from 89 studies. It is derived from the open alkali-activated concrete
dataset published by Torres et al. (2023), with additional curation and the chemistry
descriptors used in this study.

| | |
|---|---|
| Records | 2370 |
| Unique mixtures | 1226 |
| Fly ash only | 1338 records |
| GGBFS only | 318 records |
| Blended | 714 records |
| Compressive strength | 0.91 to 86.33 MPa |
| Model inputs | 16, including chemistry descriptors |

The original dataset is available at https://doi.org/10.5281/zenodo.7805018 under CC BY 4.0.
If you use the data, please cite Torres et al. (2023).

---

## Running the notebook

The notebook was developed in Google Colab on a CPU runtime and runs top to bottom without
modification. Cell outputs have been cleared to keep the file small, so run all cells to
regenerate them.

**Google Colab.** Open the notebook, upload the CSV when prompted, and run all cells.

**Locally.**

```bash
git clone https://github.com/aafshin/geopolymer-aac-ml-optimization.git
cd geopolymer-aac-ml-optimization
pip install -r requirements.txt
jupyter notebook notebooks/geopolymer_ml_optimization.ipynb
```

Random seed 42 is fixed throughout, so the results are reproducible.

---

## Notebook structure

| Section | Contents |
|---|---|
| Data preparation | Loading, cleaning, chemistry descriptor construction |
| Model development | Five base learners, five hyperparameter optimizers, 25 combinations |
| Statistical comparison | Friedman test across validation folds |
| Interpretation | SHAP analysis of the selected surrogate |
| Conformal prediction | Normalized split conformal, one-sided lower bound |
| Optimization, scenario 1 | NSGA-II under ambient curing only |
| Optimization, scenario 2 | NSGA-II with curing as a decision variable |
| Price sensitivity | Fly ash to slag price ratio sweep |
| Benchmarking | Comparison against portland cement concrete at matched grades |
| Figures and tables | All figures and tables reported in the study |

Both optimization scenarios must be run in the same session, since the figure and table cells
draw on results from each.

**Runtime note.** The NSGA-II runs use a population of 600 over 1500 generations across
multiple random seeds and take a long time on a CPU runtime. The price sensitivity sweep runs a
separate optimization at each of seven price points.

---

## Emission, energy, and cost factors

Emission factors follow Torres et al. (2023), who take them from Alsalman et al. (2021).
Embodied energy factors follow Alsalman et al. (2021). Unit costs are compiled from published
values and current United States market data. Full values and sources are given in the paper.

Because relative precursor prices vary by region, the fly ash price is swept across a range
spanning both orderings, and the resulting shift in precursor selection is reported.

---

## References

Alsalman, A., Assi, L.N., Kareem, R.S., Carter, K., Ziehl, P. (2021). Energy and CO2 emission
assessments of alkali-activated concrete and ordinary Portland cement concrete: A comparative
analysis of different grades of concrete. *Cleaner Environmental Systems*, 3, 100047.

Torres, B.M., Völker, C., Firdous, R. (2023). Concreting a sustainable future: A dataset of
alkali-activated concrete and its properties. *Data in Brief*, 50, 109525.

---

## License

Code is released under the MIT License. The dataset is redistributed under CC BY 4.0 in line
with its original license.

---

## Contact

Abolfazl Afshin, University of Mississippi. aafshin@go.olemiss.edu

Questions and issues are welcome through the repository issue tracker.
