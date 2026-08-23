# Multi-Class News Article Classification

Mahir Al Muntaqim ([mahiralmuntaqim](https://github.com/mahiralmuntaqim)),
Mohammad Hasibul Amin ([MohammadHasibulAmin](https://github.com/MohammadHasibulAmin)),
Fabiha Tarannum Areena ([FabihaTarannumA](https://github.com/FabihaTarannumA)),
Zawad Ahsan ([ZeddhD](https://github.com/ZeddhD))

CSE440 Natural Language Processing II, BRAC University.

## What this is

We compare ten text classification models, spanning classical, recurrent and
transformer families, on the 20 Newsgroups corpus. Every model is trained on the same
splits, scored by the same evaluation module, and compared on test macro-F1.

## Results

Ranked by test macro-F1, read from `results/tables/final_comparison.csv`.

| Rank | Model | Config | Tier | Embedding | Test Accuracy | Test Macro-F1 | Owner |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | BERT-Base | B3 | transformer | wordpiece | 0.7345 | 0.7225 | Zawad |
| 2 | Logistic Regression | LR-C2 | classical | tfidf_clean | 0.6982 | 0.6852 | Hasib |
| 3 | Multinomial NB | NB-C2 | classical | tfidf_clean | 0.7038 | 0.6843 | Hasib |
| 4 | Bi-LSTM | S3 | recurrent | word2vec | 0.6767 | 0.6627 | Fabiha |
| 5 | LSTM | S3 | recurrent | word2vec | 0.6720 | 0.6551 | Fabiha |
| 6 | Bi-GRU | S3 | recurrent | word2vec | 0.6409 | 0.6304 | Zawad |
| 7 | GRU | S3 | recurrent | word2vec | 0.6304 | 0.6214 | Zawad |
| 8 | Random Forest | RF-C2 | classical | tfidf_clean | 0.6373 | 0.6134 | Hasib |
| 9 | Bi-SimpleRNN | S3 | recurrent | word2vec | 0.4683 | 0.4328 | Hasib |
| 10 | SimpleRNN | S3 | recurrent | word2vec | 0.3912 | 0.3405 | Hasib |

## Findings

**Embedding coverage did not predict embedding usefulness.** Word2Vec covers 99.995%
of the vocabulary against GloVe's 87.32%, but the two ungated recurrent models
(SimpleRNN, Bi-SimpleRNN) preferred Word2Vec while all four gated models (LSTM,
Bi-LSTM, GRU, Bi-GRU) preferred GloVe. Word2Vec here was trained on roughly 9,000
project documents, so every word has a vector but each rests on little evidence. GloVe
was estimated from six billion tokens of general English. A model that cannot build
context depends on token identity and prefers a noisy vector over a missing one; a
model that can build context exploits the better-estimated vectors instead.

**Sequence length was not a binding constraint.** The BERT truncation ablation cut
truncated documents from 24.4% to 9.1%, seeing 15.2% more of the corpus, and macro-F1
moved by only +0.0016 for 1.85x the training time. Bidirectional gains point the same
way: +0.0091 for the GRU pair and +0.0077 for the LSTM pair, against +0.0923 for
SimpleRNN, which is the one architecture that cannot retain early tokens on its own.
Topic signal in these posts is front-loaded.

**Logistic Regression beat BERT on the religion classes.** Inside the `comp.*` block
BERT keeps 0.727 of each class on average against Logistic Regression's 0.673. Inside
the religion block (`alt.atheism`, `soc.religion.christian`, `talk.religion.misc`) the
order flips: Logistic Regression reaches 0.519 against BERT's 0.511. The `comp.*`
classes are separated by what a word means in context, which favours attention. The
religion classes are separated by which terms appear at all, which is what TF-IDF
measures directly.

## Repository layout

```
notebooks/          Ten training/analysis notebooks plus the merged submission notebook
src/                 Shared evaluation module used by every notebook
results/
  runs/              Per-member hyperparameter run logs
  reports/           Per-model test set evaluation reports (JSON)
  tables/            Aggregated comparison tables (CSV)
figures/             Saved plots, grouped by project phase
splits/              Frozen train/val/test splits (not tracked, see below)
representations/     Frozen embeddings and vectorizers (not tracked, see below)
```

## Notebook to author mapping

| Notebook | Author |
| --- | --- |
| `notebooks/01_phase0_data_and_representations.ipynb` | Mahir |
| `notebooks/02_classical_and_simplernn.ipynb` | Hasib |
| `notebooks/03_lstm.ipynb` | Fabiha |
| `notebooks/04_gru_and_bert.ipynb` | Zawad |
| `notebooks/05_final_analysis.ipynb` | Zawad |
| `notebooks/merge.ipynb` | Zawad |
| `notebooks/submission/02_23201151_23201409_23201042_23201136.ipynb` | Merged submission |

## Reproducing

1. Install dependencies: `pip install -r requirements.txt` (scikit-learn, tensorflow,
   transformers, pandas, numpy, gensim).
2. Download `glove.6B.50d.txt` from the
   [GloVe project page](https://nlp.stanford.edu/projects/glove/) (the 6B, 50d file)
   and place it at the repository root.
3. Run `notebooks/01_phase0_data_and_representations.ipynb` first. It builds
   `splits/` and `representations/`, which every later notebook depends on.
4. Run `notebooks/02_classical_and_simplernn.ipynb`, `notebooks/03_lstm.ipynb`, and
   `notebooks/04_gru_and_bert.ipynb` in any order.
5. Run `notebooks/05_final_analysis.ipynb` last. It reads the saved run logs and
   report JSONs in `results/` and does not retrain anything.

All notebooks were run on Google Colab with a T4 GPU.
