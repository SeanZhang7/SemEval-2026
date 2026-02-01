# Develop Log

# 

# Feature Used

- Text Embedding
- LIWC Features
- Item Scores
- User_ID Embedding

## Methods to Extract Features

```python
SemEval-2026/extremism/item-scoring
SemEval-2026/liwc.py
```

# Data Processing

- Observations: **5,285** (language, EMA emotion pairs)
- Users: **182**
- Average number of texts per user **72.8** (Average essays per users: **53.1**; Average feeling-words per user: **48.3**)
- Median number of texts per user **35.0** (Median essays per users: **18.00**; Median feeling-words per user: **18.00**)

The training and evaluation data consist of 5,285 longitudinal texts (“ecological essays and feeling words”) written by 182 authors collected over multiple years (2021 – 2024), consisting of real‑time essays and feeling words (e.g., happy, calm, sad, etc.) written by U.S. service‑industry workers about “how they are feeling”. 

(https://www.codabench.org/competitions/9963/#/pages-tab)

## Data Distribution:

![image.png](Develop%20Log/image.png)

## Processing Script

```python
SemEval-2026/subTask1/data_processing.ipynb
```

- Separate Training Data into train set and val set randomly, which means there are some users in both train and val (2211 : 553).
- Generate LIWC Features, store in ‘task1_LIWC_train/val.pickle’ (90 features).
- Generate Item Score Features, store in ‘task1_Arousal/ValenceSim_train/val’ (5 features).
- Generate text embedding Features, store in ‘task1_embedding_train/val.pickle’ (384 features).
- Same steps for Testing data.

# Subtask 1

## LIWC Baseline

```python
SemEval-2026/subTask1/Baselines/LIWC_baseline.ipynb
```

### Features:

LIWC words counts + User_id embedding

### Data Shape:

LIWC train shape: (2211, 79+32)
LIWC val shape: (553, 79+32)

### Modle:

4 Layers MLP

### Performance:

![image.png](Develop%20Log/image%201.png)

| Valence - Train MSE | 0.500625 | Valence - Val MSE | 0.831603 |
| --- | --- | --- | --- |
| Arousal  - Train MSE | 0.289624 | Arousal  - Val MSE | 0.407526 |
| Valence - Train MAE |  0.552294 | Valence - Val MAE | 0.699679 |
| Arousal  - Train MAE | 0.422752 | Arousal  - Train MAE | 0.499812 |

## Embedding Baseline

```python
SemEval-2026/subTask1/Baselines/embedding_baseline.ipynb
```

### Features:

Text Embedding + User_id embedding

### Data Shape:

Embedding train shape: (2211, 384+32)
Embedding val shape: (553, 384+32)

### Modle:

4 Layers MLP

### Performance:

![image.png](Develop%20Log/image%202.png)

| Valence - Train MSE | 0.300632 | Valence - Val MSE | 0.729933 |
| --- | --- | --- | --- |
| Arousal  - Train MSE | 0.208794 | Arousal  - Val MSE | 0.399297 |
| Valence - Train MAE |  0.411321 | Valence - Val MAE | 0.650955 |
| Arousal  - Train MAE | 0.350806 | Arousal  - Train MAE | 0.489052 |

## Item Score Baseline

```python
SemEval-2026/subTask1/Baselines/item_score_baseline.ipynb
```

### Features:

Item Scores for text and archetypes of description of Valence and arousal level + User_id embedding

### Data Shape:

Embedding train shape: (2211, 10+32)
Embedding val shape: (553, 10+32)

### Modle:

4 Layers MLP

### Performance:

![image.png](Develop%20Log/image%203.png)

| Valence - Train MSE | 0.605143 | Valence - Val MSE | 0.705021 |
| --- | --- | --- | --- |
| Arousal  - Train MSE | 0.378295 | Arousal  - Val MSE | 0.462785 |
| Valence - Train MAE | 0.590322 | Valence - Val MAE | 0.639706 |
| Arousal  - Train MAE | 0.484828 | Arousal  - Train MAE | 0.545395 |

## Combine All Features:

```python
SemEval-2026/subTask1/Baselines/full_baseline.ipynb
```

### Features:

All Features in Baseline + User_id embedding

### Data Shape:

Embedding train shape: (2211, 473+32)
Embedding val shape: (553, 473+32)

### Modle:

4 Layers MLP

### Performance:

![image.png](Develop%20Log/image%204.png)

| Valence - Train MSE | 0.310411 | Valence - Val MSE | 0.717461 |
| --- | --- | --- | --- |
| Arousal  - Train MSE | 0.220216 | Arousal  - Val MSE | 0.389909 |
| Valence - Train MAE | 0.416968 | Valence - Val MAE | 0.646991 |
| Arousal  - Train MAE | 0.357697 | Arousal  - Train MAE | 0.483780 |

![image.png](Develop%20Log/image%205.png)

## Testing

```python
SemEval-2026/subTask1/Test.ipynb
```

Use the model trained in full_baseline:

```python
SemEval-2026/subTask1/Baselines/best_model.pt
```

Use the scalers used in full_baseline:

```python
SemEval-2026/subTask1/scaler_liwc.pkl
SemEval-2026/subTask1/scaler_sim.pkl
```

Use the User_id embedding and User_id map in full_baseline:

```python
SemEval-2026/subTask1/Baselines/trained_user_embeddings.npy
SemEval-2026/subTask1/Baselines/user_id_map.pkl
```

## Testing Distribution:

![image.png](Develop%20Log/image%206.png)