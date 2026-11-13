# Data

The data files are not included in this repository and are available from the authors upon
request. Place them in this folder to run the notebooks.

All files are semicolon-separated, use a decimal comma and are UTF-8 encoded with a byte order
mark. Read them with:

```python
pd.read_csv(path, sep=";", decimal=",", encoding="utf-8-sig")
```

## What is not included

The files are limited to the variables the analyses use. Left out are: participants' Bluesky DIDs,
panel and login identifiers, open survey answers, the handles participants typed in the surveys,
income and employment, and any post or article links. Participants appear only by the handle of
the Bluesky study account the research team created for them (`newsflowsuserNNN.bsky.social`).

## Survey and activity data

| File | Sample | Used by |
|---|---|---|
| `onboarding_sample_round1.csv` | Completed the onboarding survey and active on the feed on at least two days (N = 74) | 01, 02, 04 |
| `offboarding_sample_round1.csv` | Also completed the offboarding survey (N = 56) | 01, 02, 05, 06, 07 |

One row per participant and day, from the participant's first day on the feed. Survey answers
repeat on every row of a participant. The analyses count activity up to and including
`offboarding_received_date`.

**Activity**

| Column | Description |
|---|---|
| `handle` | Bluesky study account of the participant |
| `arm` | Condition: `K` = control (most recent article per event cluster), `M` = treatment (diversity-aware) |
| `first_day` | First day the participant used the feed |
| `day` | Calendar day of the row |
| `offboarding_received_date` | Day the participant received the offboarding survey |
| `active` | Whether the participant opened their assigned feed that day |
| `reactions` | Likes, reposts, replies and quotes the participant gave to news posts in the feed that day |

**Pre-survey and onboarding survey**

| Column | Description |
|---|---|
| `sd_age_years` | Age in years. One missing value, in the treatment condition, is mean-imputed |
| `sd_gender` | 1 = man, 2 = woman, 3 = other |
| `sd_edu_be_rec` | Education: 1 = none or primary, 2 = general secondary not completed, 3 = technical, vocational or arts secondary not completed, 4 = general secondary completed, 5 = technical, vocational or arts secondary completed, 6 = higher non-university, 7 = university. Codes 1 to 3, 4 to 5 and 6 to 7 form the three levels in Table 1 |
| `news_interest_` | Interest in news (1 = not interested at all, 5 = a great deal of interest) |
| `interest_politics_` | Interest in politics (1 to 5, as above) |
| `ideo_lr_1` | Left-right self-placement (−5 = left, 5 = right) |
| `inst_trust_1` | Trust in social media (1 = no trust at all, 5 = a great deal of trust) |
| `inst_trust_2` | Trust in news media (1 to 5, as above) |
| `internet_use` | Frequency of internet use (1 = less than once a week, 8 = more than 10 times per day) |
| `news_use_6` | News use on social media (1 = never, 7 = multiple times per day) |
| `div_values_1` to `div_values_7` | Diversity-seeking values: how important respondents find it that people receive each kind of news (1 = not at all important, 5 = extremely important) |
| `div_traits_1` to `div_traits_7` | Diversity-seeking traits: how often respondents encounter each kind of news when looking for news themselves (1 = never, 5 = always) |
| `div_values_mean`, `div_traits_mean` | Means of the seven items above |
| `div_perceived__2`, `div_perceived__3` | Perceived diversity of national news media: attention to a diverse range of issues, and of politicians and parties (1 = completely disagree, 5 = completely agree) |
| `div_perceived_mean` | Mean of the four perceived-diversity items |

The survey items are listed in Appendix A of the paper.

**Offboarding survey** (`offboarding_sample_round1.csv` only; 1 = completely disagree, 5 = completely agree)

| Column | Description |
|---|---|
| `user_satisfaction_1` | I would like to use the feed again |
| `user_satisfaction_2` | The news posts in the feed were of good quality |
| `user_satisfaction_3` | I was satisfied with the selection of news posts in the feed |
| `topics` | The news posts covered a wide range of topics |
| `parties` | The news posts featured political actors from a wide range of parties |

## Treatment-check data

Feed-level data of the two feeds between 22 September and 18 October 2026. They contain no
participant data. Used by notebook 03.

**`treatment_check_rankings_round1.csv`**: one row per ranking cycle, condition and level

| Column | Description |
|---|---|
| `cycle_id` | Ranking cycle; both feeds were ranked in the same cycle every 30 minutes |
| `arm` | `K` = control, `M` = treatment |
| `completed_at` | Time the cycle finished (UTC) |
| `day` | Calendar day of the cycle (Belgian time) |
| `level` | Part of the feed: `top10` and `top20` = the first 10 and 20 political clusters, `tier_end` = all political clusters |
| `political_tier_end` | Number of political clusters in the feed |
| `n_political` | Political articles at this level |
| `n_with_ideology` | Political articles that mention at least one party with a left, center or right category |
| `n_left`, `n_center`, `n_right` | Articles mentioning at least one party of each category |
| `votes` | `n_left + n_center + n_right` |
| `shannon` | Shannon entropy (H) of the left, center and right shares |
| `n_differ` | Positions in the political part of the feed where the two feeds served different articles |
| `n_differ_outside_tier` | The same, outside the political part of the feed |

**`treatment_check_clusters_round1.csv`**: one row per political cluster in the last cycle of each day

| Column | Description |
|---|---|
| `cycle_id` | Ranking cycle |
| `n_ideologies` | Number of ideological categories the cluster's articles mention (0 to 3) |
| `n_left`, `n_center`, `n_right` | Articles in the cluster mentioning a party of each category |

**`treatment_check_sources_round1.csv`**: one row per article served in the last cycle of each day

| Column | Description |
|---|---|
| `cycle_id` | Ranking cycle |
| `arm` | `K` = control, `M` = treatment |
| `rank` | Position in the feed |
| `source` | Domain of the news outlet |

**`party_positions_ches2024.csv`**: the 13 Belgian parties in the ranker's reference

| Column | Description |
|---|---|
| `party` | Party abbreviation |
| `lrgen` | General left-right position in the 2024 Chapel Hill Expert Survey (0 = left, 10 = right) |
