# Develop Log

# 

# Literature Review

- Emotion Flow
- Affective Circumplex
- Factors that may affect Valence and Arousal

# Useful Features

## Methods to Extract Features

# Data Processing

## SubTask 1

Run all the cells in 

```jsx
SemEval-2026/subTask1/data_processing.ipynb
```

## SubTask 2a

Run all the cells in 

```jsx
SemEval-2026/subTask2a/data_processing.ipynb
```

## SubTask 2b

Run all the cells in 

```jsx
SemEval-2026/subTask2b/data_processing.ipynb
```

# Subtask 1

## LIWC Baseline

### Features:

LIWC words counts

### Data Shape:

LIWC train shape: (2211, 79+32)
LIWC val shape: (553, 79+32)

(LIWC features+User_id embedding)

### Modle:

4 Layers MLP

### Performance:

![image.png](Develop%20Log/image.png)

| Valence - Train MSE | 0.500625 | Valence - Val MSE | 0.831603 |
| --- | --- | --- | --- |
| Arousal  - Train MSE | 0.289624 | Arousal  - Val MSE | 0.407526 |
| Valence - Train MAE |  0.552294 | Valence - Val MAE | 0.699679 |
| Arousal  - Train MAE | 0.422752 | Arousal  - Train MAE | 0.499812 |

## Embedding Baseline

### Features:

Text Embedding

### Data Shape:

Embedding train shape: (2211, 384+32)
Embedding val shape: (553, 384+32)

(Text embedding +User_id embedding)

### Modle:

4 Layers MLP

### Performance:

![image.png](Develop%20Log/image%201.png)

| Valence - Train MSE | 0.300632 | Valence - Val MSE | 0.729933 |
| --- | --- | --- | --- |
| Arousal  - Train MSE | 0.208794 | Arousal  - Val MSE | 0.399297 |
| Valence - Train MAE |  0.411321 | Valence - Val MAE | 0.650955 |
| Arousal  - Train MAE | 0.350806 | Arousal  - Train MAE | 0.489052 |

## Item Score Baseline

### Features:

Item Scores for text and archetypes of description of Valence and arousal level

### Data Shape:

Embedding train shape: (2211, 10+32)
Embedding val shape: (553, 10+32)

(5 Valence item scores + 5 Arousal item scores +User_id embedding)

### Modle:

4 Layers MLP

### Performance:

![image.png](Develop%20Log/image%202.png)

| Valence - Train MSE | 0.605143 | Valence - Val MSE | 0.705021 |
| --- | --- | --- | --- |
| Arousal  - Train MSE | 0.378295 | Arousal  - Val MSE | 0.462785 |
| Valence - Train MAE | 0.590322 | Valence - Val MAE | 0.639706 |
| Arousal  - Train MAE | 0.484828 | Arousal  - Train MAE | 0.545395 |

## Combine All Features:

### Features:

ALl Features in Baseline

### Data Shape:

Embedding train shape: (2211, 473+32)
Embedding val shape: (553, 473+32)

### Modle:

4 Layers MLP

### Performance:

![image.png](Develop%20Log/image%203.png)

| Valence - Train MSE | 0.300632 | Valence - Val MSE | 0.729933 |
| --- | --- | --- | --- |
| Arousal  - Train MSE | 0.208794 | Arousal  - Val MSE | 0.399297 |
| Valence - Train MAE | 0.411321 | Valence - Val MAE | 0.650955 |
| Arousal  - Train MAE | 0.350806 | Arousal  - Train MAE | 0.489052 |