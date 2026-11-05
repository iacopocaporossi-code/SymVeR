# SymVeR
Symbolic Velocity Recurrence: identifying slow–fast hierarchies and delays from time series.

SymVeR identifies, directly from multivariate time series, which of two coupled variables evolves on the slower timescale and acts as a parameter-like variable for the other, together with their interaction delay. It works on the direction of change of each series (the ternary sequence sgn(x_t − x_{t−1})) and combines three recurrence measures:

the trapping time of the recurrence plot of the raw series (timescale);
the laminarity of the recurrence plot of the ternary series (smoothness of the evolution);
the diagonal cross recurrence profile of the ternary series (coupling and delay).

Coupling is tested against circular-shift surrogates, the timescale hierarchy by joint moving-block bootstrap, and multiple comparisons are corrected with a two-stage Benjamini–Hochberg procedure. Each pair of variables is classified as driver → response (with delay), synchronous slow–fast, coupled with no timescale hierarchy, or no coupling. For the identified pairs, the estimated delay is used to draw a lag-corrected hysteresis profile of the response against its driver.

**Repository content:**
-  symver.ipynb                    # the complete analysis (method, validation, applications, figures)
-  ESMdata.csv                     # EMA data (see "Data" below)
-  New_30minDataset_SMEAR.csv      # SMEAR II half-hourly data (see "Data" below)
-  results/                        # CSV files with the results reported in the paper

The notebook reads the data files from its own folder and writes its outputs (CSV files and figures) to the same folder. The results/ folder contains a copy of the outputs used in the paper.

**How to run:**
Open symver.ipynb and run the cell in order. 

The notebook is organized in parts:
- A.1 - A.6: Recurrence measures, coupling tests, bootstrap, Benjamini-Hochberg, full procedure, hystreresis profile
- B.1 - B.8: Synthetic validation
- B.9 - B.10: Robustness and sensitivity analysis
- C.1 - C.3: Application to EMA and SmearII data
- D.1 - D.5: Hysteresis profile of EMA and SmearII data

Approximate run times on a laptop: Part A < 1 s; Part B about 30 min (about 4 min with QUICK = True); B.9 about 50 min; B.10 about 40 min; Part C a few minutes. With QUICK = True (and ROB_QUICK, SAMP_QUICK in B.9 and B.10) fewer realizations and bootstrap replicates are used: the results are indicative only and do not reproduce the paper exactly.

All random generators are seeded, so the full runs reproduce the results of the paper.

**Data**

EMA. Single-subject experience sampling data of an individual with a history of major depression who gradually discontinued antidepressant medication (Wichers et al., 2016). The data are openly available from Kossakowski et al. (2017), Journal of Open Psychology Data, 5(1), 1. Download ESMdata.csv from the original source and place it in the notebook folder.

SMEAR II. Half-hourly measurements from the SMEAR II station (Hyytiälä, Finland), downloaded from the SmartSMEAR portal (https://smear.avaa.csc.fi/) for summer 2025: gross primary production (HYY_EDDY233.GPP), photosynthetically active radiation (HYY_RAD.PAR), air temperature (HYY_META.Tst270) and relative humidity (HYY_META.RHTd). SMEAR data are distributed under the conditions stated on the portal; please cite Hari & Kulmala (2005) and Junninen et al. (2009) when using them.

**Results**

The results/ folder contains:
- validation_data/ : synthetic datasets of every scenario
- validation_results.csv and validation_detail.csv are the outcome of every pair I the every realization
- hysteresis_test_results.csv contains the data used to generate Figure S3 in the supplementary materials
- robustness_results.csv, robustness_length.csv, robustness_rr.csv, sampling_results.csv, sampling_table.csv contain the robustness and sensitivity tests
- comparison_timescale.csv, comparison_timescale_detail.csv contain the comparison between SymVeR and autocorrelation times
- EMA_symver_results.csv and SMEAR30_symver_results.csv contain the classification of all pairs in the EMA and SMEAR II datasets respectively.
- RR_results_EMA.csv contains the recurrence measures of all the SymVeR's outputs of the EMA dataset.
