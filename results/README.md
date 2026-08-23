# Results

## Run logs (`runs/`)

Three files, one per member who trained recurrent or classical models:
`runs_hasib.csv` (18 rows), `runs_fabiha.csv` (8 rows), `runs_zawad.csv` (10 rows).
36 rows total.

Each row is one training run and carries: `run_id`, `owner`, `notebook`, `tier`,
`model`, `config`, `embedding`, architecture hyperparameters (`units`, `dropout`,
`trainable_emb`, `batch_size`, `learning_rate`, `epochs_run`, `best_epoch`,
`n_params`, `hyperparams`), validation and test metrics (`val_loss`,
`val_accuracy`, `val_macro_f1`, `test_accuracy`, `test_macro_f1`,
`test_weighted_f1`), `train_time_s`, `dataset_checksum`, `timestamp`, and `notes`.

All 36 rows carry the same `dataset_checksum`, which proves every model in the
project was trained and evaluated against the same data splits.

## Reports (`reports/`)

Eleven JSON files, one per evaluated model configuration, named
`test_<model>_<config>.json`. Each contains the full test-set evaluation for that
run: per-class precision/recall/F1, the confusion matrix, and the aggregate
accuracy and macro/weighted F1 used in the comparison tables.

Produced by:

| Member | Reports |
| --- | --- |
| Hasib | `test_LogisticRegression_LR-C2.json`, `test_MultinomialNB_NB-C2.json`, `test_RandomForest_RF-C2.json`, `test_SimpleRNN_S3.json`, `test_BiSimpleRNN_S3.json` |
| Fabiha | `test_LSTM_S3.json`, `test_Bi-LSTM_S3.json` |
| Zawad | `test_GRU_S3.json`, `test_Bi-GRU_S3.json`, `test_BERT-Base_B3.json` |

## Tables (`tables/`)

- `final_comparison.csv` — all ten required models ranked by test macro-F1.
- `tuning_table_all.csv` — every tuning run recorded across all three run logs.
- `test_comparison_fabiha.csv`, `test_comparison_zawad.csv` — per-member subsets of
  the final comparison, produced alongside each member's notebook.
