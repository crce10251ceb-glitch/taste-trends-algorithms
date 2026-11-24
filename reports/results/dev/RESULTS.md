# Results - `dev` mode

_Generated automatically by `src/report.py` from the pipeline's output files._

Spark version: 4.0.1 · sample fraction: 1.0

| Stage | Seconds |
|---|---|
| ingestion | 19.3 |
| preprocessing | 20.8 |
| eda | 30.5 |
| training | 102.6 |
| evaluation | 10.7 |
| total | 197.1 |

## Dataset

| Measure | Value |
|---|---|
| Ratings | 100,836 |
| Users | 610 |
| Movies in catalogue | 9,742 |
| Movies with ≥ 1 rating | 9,724 |
| Tags | 3,683 |
| Average rating | 3.5016 |
| Matrix sparsity (%) | 98.3000 |
| First rating | 1996-03-29T18:36:55 |
| Last rating | 2018-09-24T14:27:30 |

## Model

ALS rank = **8**, regParam = **0.2**, maxIter = 15; trained in 11.8 s; factors for 610 users and 8,991 movies.

### Hyper-parameter search (validation RMSE)

| rank | reg_param | max_iter | val_rmse | seconds |
|---|---|---|---|---|
| 8 | 0.2000 | 10 | 0.8792 | 10.6000 |
| 16 | 0.2000 | 10 | 0.8800 | 10.0000 |
| 16 | 0.1000 | 10 | 0.8938 | 11.2000 |
| 8 | 0.1000 | 10 | 0.8941 | 10.8000 |
| 8 | 0.0500 | 10 | 0.9618 | 17.8000 |
| 16 | 0.0500 | 10 | 0.9856 | 10.8000 |

## Rating prediction (RMSE, lower is better)

Scored 19,068 of 19,870 test ratings (802 dropped because the user or movie never appeared in training - cold start).

| Model | RMSE |
|---|---|
| ALS | 0.8829 |
| Baseline μ + b_u + b_i | 0.8691 |
| Baseline global mean | 1.0434 |

## Top-10 recommendation quality (590 test users, relevant = rated ≥ 4.0)

| model | precision_at_10 | recall_at_10 | ndcg_at_10 | hit_rate_at_10 | coverage | arp | head_share | tail_share | gini_exposure |
|---|---|---|---|---|---|---|---|---|---|
| ALS | 0.0002 | 0.0008 | 0.0010 | 0.0017 | 0.0195 | 1.2153 | 0.0000 | 0.9980 | 0.9972 |
| Popularity | 0.1207 | 0.0932 | 0.1591 | 0.5458 | 0.0059 | 195.6402 | 1.0000 | 0.0000 | 0.9980 |
| Random | 0.0029 | 0.0014 | 0.0033 | 0.0288 | 0.4806 | 8.5880 | 0.0675 | 0.7622 | 0.6161 |

Average popularity of movies in users' own histories (ARP of profiles): 47.2 ratings. Popularity lift (ARP of recommendations ÷ ARP of profiles): ALS 0.03, Popularity 4.14, Random 0.18

### ALS lists for every user

610 users · catalogue coverage 0.0195 · Head share 0.0% · Tail share 99.8% · Gini 0.9972
