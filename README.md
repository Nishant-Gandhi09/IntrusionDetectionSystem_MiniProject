# Explainable Network Intrusion Detection

This project builds and evaluates a binary network intrusion detector using the UNSW-NB15 dataset. The notebook implements Parts A–G of the mini-project brief.

## Dataset

Use the UNSW-NB15 'training-set.csv' and 'testing-set.csv' files from the [UNSW-NB15 dataset page](https://research.unsw.edu.au/projects/unsw-nb15-dataset). Place the files at:

'''text
data/UNSW_NB15_training-set.csv
data/UNSW_NB15_testing-set.csv
'''

The notebook combines these files, removes exact duplicate rows, cleans feature values, then creates the stratified 60/20/20 split required by the assignment. It uses all available rows ('SAMPLE_SIZE = None').

The target is binary: '0 = Normal' and '1 = Attack'. 'attack_cat' is retained for reporting attack-category counts but is excluded from model inputs to avoid target leakage.

## Implemented Parts

- **Part A:** Describes the detection problem; loads and cleans the CSV files; reports dataset size, class balance, missing feature values, a class-balance plot, and a stratified 60/20/20 train/validation/test split. A majority-class baseline is reported with the model metrics.
- **Part B:** Trains Logistic Regression and Decision Tree models as interpretable baselines and a Random Forest as the black-box model. Preprocessing is fitted on training data. Candidate settings are compared using validation Macro-F1; the held-out test evaluation is at the notebook's end.
- **Part C:** Compares the full-label Random Forest with a Random Forest trained on 10% of training labels and a pseudo-labeling approach using the remaining training features. Confidence cutoffs are selected on validation data.
- **Part D:** Explains model behavior using feature importance, SHAP, and LIME. It compares important features across models, shows local explanations for selected validation flows, and checks SHAP fidelity and LIME stability.
- **Part E:** Tests robustness to missing feature information by replacing increasing fractions of validation features with training-set medians or modes. Results are averaged over repeated trials and reported for Logistic Regression, Decision Tree, and Random Forest.
- **Part F:** Builds an interpretable Belief Rule Base from 'sttl' and 'dttl'. Nine rules are estimated from training data, combined with Evidential Reasoning, and compared with two-feature tree and forest models on validation data. The part also demonstrates how the rule base represents uncertainty when an input is missing.
- **Part G:** Tests adaptability to unseen attack categories by training a Random Forest without one attack type at a time, measuring performance on the held-out test partition, then retraining with 100 labelled training examples of the hidden type across three random seeds.

## Environment and Run

Python 3.10 or newer is recommended. Install the notebook dependencies:

'''bash
python3 -m venv .venv
source .venv/bin/activate
pip install numpy pandas matplotlib scikit-learn jupyter shap lime
'''

Open 'intrusion_detection.ipynb' in VS Code or Jupyter with the project directory as the working directory, then run all cells from top to bottom. Keep the final held-out test-evaluation cell at the end of the notebook as later project parts are added. The notebook currently uses the full cleaned dataset; runtime depends on the local machine.

## Main Files

- 'intrusion_detection.ipynb': executable experiment
- 'PROJECT_NOTES.md': explanation of the implementation, split, validation choices, and observed results
- 'data/': UNSW-NB15 CSV files
- 'results/': reserved for project outputs
