# Chandra Automation Pipeline

Automated pipeline for detecting energy-independent transit candidates in Chandra X-ray light curves, using Bayesian Blocks and a random forest, to search for extragalactic planet candidates.

## Overview

Only one extragalactic planet candidate (M51-ULS-1b) is known, and no automated tool exists for searching large X-ray archives for more. This pipeline works on event lists from the Chandra Source Catalog (CSC) and:

1. **Preprocesses data** with CIAO and `chandralc`: unpacks archives, builds light curves in the broad, soft, medium and hard bands, and removes HRC data and low-count observations.
2. **Segments each event list** with Astropy's Bayesian Blocks algorithm (`fitness='events'`).
3. **Extracts per-block features:** duration, event count, count rate, and the percentage of the observation's events in the block.
4. **Classifies each block** with a random forest: `0` = no transit, `1` = short-duration transit, `2` = long-duration transit.
5. **Tests energy independence** of predicted transits with a one-way ANOVA across the soft, medium and hard bands (`p < 0.05` means energy dependent).

## Repository contents

| File | Description |
|------|-------------|
| `Chandra_Automation_Pipeline.ipynb` | Full pipeline notebook, in the order: data extraction, Bayesian Blocks and event lists, feature engineering, random forest, energy-independence testing |

## Requirements

- Python 3.9+
- [CIAO](https://cxc.cfa.harvard.edu/ciao/) and [`chandralc`](https://github.com/sammarth-k/chandralc) (light-curve generation)
- Python packages: `numpy`, `pandas`, `matplotlib`, `seaborn`, `astropy`, `scipy`, `scikit-learn`, `tqdm`

```bash
pip install numpy pandas matplotlib seaborn astropy scipy scikit-learn tqdm
```

## Usage

1. Download source data (`regevt3` event lists and `srcreg` files) from the [Chandra Source Catalog](https://cxc.cfa.harvard.edu/csc/).
2. Set `all_directory` at the top of each notebook section to the folder holding your downloaded sources.
3. Run the notebook sections in order.

The data are not included in this repository because of their size.

## Citation

If you use this code, please cite:

```
Alemán, E. N. (2026). Automating the Discovery of Extragalactic Planet Candidates:
A Machine-Learning Pipeline for Transit Detection in X-ray Light Curves.
```

## Acknowledgments

Mentors: Dr. Nicholas Lauersdorf and Dr. Rosanne Di Stefano. Research Science Institute (RSI) at MIT.

## License

MIT
