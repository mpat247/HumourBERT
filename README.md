# HumourBERT

Shared-private BERT architecture for humor detection and subtype-aware representation learning.

HumourBERT studies whether related text domains can share a common transformer representation while still keeping type-specific features separate. The project uses humor categories as the domains and combines a shared BERT encoder, private BERT encoders for individual humor types, and ConceptNet embeddings for external semantic information.

This was developed as an EE8228 research project at Toronto Metropolitan University.

## Approach

The main model has three parts:

- **Shared BERT encoder** for features that are useful across humor types.
- **Private BERT encoders** for type-specific representations.
- **ConceptNet features** concatenated with the shared and private representations before classification.

The repository also contains earlier shared-only and shared-private experiments used to build up to the ConceptNet version.

## Data and evaluation

The preprocessing code includes a balanced 150,000-sample binary classification setup and stratified train/validation/test splits for the shared-private experiments.

One recorded shared-private run in `output/reports/sharedprivate1results.txt` reached **95.44% test accuracy** and **95.44% weighted F1**. The repository keeps the evaluation outputs used during development; trained model checkpoints are excluded because of their size.

## Repository structure

```text
.
├── ConceptNetSharedPrivate.ipynb      # ConceptNet + shared-private experiment
├── SharedPrivateArchitecture.ipynb    # Shared-private BERT experiment
├── SharedLayer.ipynb                  # Shared BERT experiments
├── src/
│   ├── data.py                        # preprocessing and dataset utilities
│   ├── models.py                      # shared-private model
│   ├── training.py                    # training and evaluation utilities
│   ├── final_data.py                  # final dataset pipeline
│   ├── final_models.py                # ConceptNet-enhanced model
│   ├── final_training.py              # final training utilities
│   └── final_utils.py                 # supporting utilities
├── data/                              # processed research data and caches
├── output/reports/                    # saved evaluation results
└── requirements.txt
```

## Setup

```bash
python -m venv .venv
source .venv/bin/activate       # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

The notebooks contain the original experiment flow. The main progression is:

1. `SharedLayer.ipynb`
2. `SharedPrivateArchitecture.ipynb`
3. `ConceptNetSharedPrivate.ipynb`

Model checkpoints are not stored in the repository, so paths to pretrained or locally trained BERT checkpoints may need to be updated before rerunning an experiment.

## Tech

Python, PyTorch, Hugging Face Transformers, BERT, ConceptNet, scikit-learn, pandas.