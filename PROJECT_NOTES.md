# Experiment notes

HumourBERT was built as an NLP research project around shared-private representation learning.

## Research question

Can a transformer learn features that transfer across related text categories while also preserving category-specific information?

Humor detection is the application used to test that question. The architecture is the main focus of the project rather than the subject matter itself.

## Model progression

### 1. Shared BERT
A shared encoder learns features across the full dataset.

### 2. Shared-private BERT
The model combines:

- one shared BERT representation
- a private BERT representation selected for the input category
- a classifier over the concatenated features

The shared branch is intended to capture common signals, while the private branches retain category-specific information.

### 3. ConceptNet-enhanced shared-private model
The final experiment augments the transformer representations with ConceptNet-derived semantic features before classification.

The final classifier therefore receives:

```text
shared BERT representation
        +
private BERT representation
        +
ConceptNet embedding
        |
        v
classification head
```

## Evaluation

A saved shared-private run reports:

- test accuracy: 95.44%
- weighted precision: 95.45%
- weighted recall: 95.44%
- weighted F1: 95.44%

These values are preserved in `output/reports/sharedprivate1results.txt`.

A separate evaluation artifact in `output/reports/evaluation_metrics.json` records a later experiment with 99.23% accuracy/F1. Because the repository does not preserve enough run metadata to confidently identify that result with a specific model configuration, it is intentionally not presented as the headline project result.

## Scope

This repository preserves the original experimental notebooks and supporting source files. It is a research/code archive rather than a packaged production library.