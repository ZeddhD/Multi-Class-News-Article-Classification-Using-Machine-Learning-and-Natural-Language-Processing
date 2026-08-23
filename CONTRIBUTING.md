# Contributing

Each member pushes their own work from their own GitHub account, so the contributor
graph reflects who actually did what.

## Ownership

| Member | GitHub | Owns |
| --- | --- | --- |
| Mahir Al Muntaqim | mahiralmuntaqim | Dataset, EDA, preprocessing, splits, all three word representations |
| Mohammad Hasibul Amin | MohammadHasibulAmin | Random Forest, Logistic Regression, Naive Bayes, SimpleRNN, Bidirectional SimpleRNN |
| Fabiha Tarannum Areena | FabihaTarannumA | LSTM, Bidirectional LSTM, and the shared evaluation module |
| Zawad Ahsan | ZeddhD | GRU, Bidirectional GRU, BERT Base, merged notebook, final analysis |

## Push order

The pushes below are ordered because later ones assume earlier ones are already on
the remote.

1. **Zawad** — skeleton: `README.md`, `CONTRIBUTING.md`, `.gitignore`,
   `results/README.md`, and the empty directory tree.
2. **Mahir** — Phase 0 notebook and its figures.
3. **Fabiha** — shared evaluation module, LSTM notebook, figures and results.
4. **Hasib** — classical and SimpleRNN notebook, figures and results.
5. **Zawad** — GRU/BERT notebook, final analysis, merge notebook, submission
   notebook, figures and results.

## Before you commit

1. Set your git identity to your own GitHub account for this repository:
   ```
   git config user.name "Your Name"
   git config user.email "you@users.noreply.github.com"
   ```
   Never commit under someone else's identity.
2. `git pull --rebase` before pushing, so you land on top of whatever the others
   have already added.
3. Push only the paths assigned to you above. Leave everyone else's paths alone.

## Do not modify

- Any `.ipynb` file's code, markdown, or outputs. If a notebook needs a change, raise
  it with the notebook's owner instead of editing it directly.
- Anything under `splits/`, `representations/`, or `src/`. These are frozen artifacts
  the results depend on, except `src/` may only be changed by its owner (Fabiha).

## Commits

Plain, descriptive, imperative commit messages. One commit per logical group of
files, not one giant commit per person.
