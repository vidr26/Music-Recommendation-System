# Music Recommendation System

Recommends the top songs for each user from their listening history, comparing popularity-based, collaborative filtering, matrix factorization, clustering and content-based approaches on the Million Song Dataset.

Completed as part of the **Applied Data Science Program**, MIT Professional Education.

- **Notebook (code and full report):** [`VidyaVasist_Final_Report_Code_Music_Recommendation_Systems.ipynb`](VidyaVasist_Final_Report_Code_Music_Recommendation_Systems.ipynb)
- **Milestone presentation:** [`VidyaVasist_Milestone_1_Music_Recommendation_Systems.pptx`](VidyaVasist_Milestone_1_Music_Recommendation_Systems.pptx)

## Problem definition

**Context: why is this problem important to solve?**
With an ever-growing number of songs available online, finding songs you will like has become tedious. Streaming platforms want users to spend more time listening, which increases revenue. A recommendation system that suggests songs based on a user's likes and dislikes, across millions of users and songs, benefits both listeners and platforms.

**Objectives: what is the intended goal?**
- Build a recommendation system that proposes the top 10 songs for a user, based on how likely they are to listen to them.
- Increase the time customers spend on the platform, and with it the company's revenue.

**Key questions**
- What kind of content are customers most likely to consume?
- Which songs are most popular, to suggest to a new user?
- Which songs are similar to an existing user's listening history?
- Which users have similar tastes, so their songs can be recommended to each other?

**Problem formulation**
- For new users with no history, recommend popular songs (a popularity-based system that handles the cold-start problem).
- For existing users, build models using collaborative filtering, matrix factorization and other methods, compare their performance, and choose the best one.

## Data

The data is the Taste Profile Subset released by the Echo Nest as part of the [Million Song Dataset](http://millionsongdataset.com/). It has two files.

**song_data**
- `song_id`: a unique id for every song
- `title`: title of the song
- `Release`: name of the released album
- `Artist_name`: name of the artist
- `year`: year of release

**count_data**
- `user_id`: a unique id for the user
- `song_id`: a unique id for the song
- `play_count`: number of times the user played the song

After keeping users who listened to at least 90 songs and songs heard by at least 120 users, and dropping play counts above 5, the modeling data has 117,876 interactions from 3,155 users on 563 songs by 232 artists.

## Evaluation setup

- Train/test split: 60/40 (`random_state = 42`).
- Models built with the [Surprise](https://surpriselib.com/) library, with hyperparameters tuned by grid-search cross-validation.
- Metrics: RMSE on predicted play count, and precision@k, recall@k and F1@k with k = 30 and a relevance threshold of 1.5 plays.
- **F1 is the primary measure**, because a good recommender has to avoid both missed songs the user would like (false negatives) and songs they won't (false positives).

## Results

| model | RMSE | precision@30 | recall@30 | F1@30 |
|---|---|---|---|---|
| User-user similarity (baseline) | 1.088 | 0.396 | 0.692 | 0.504 |
| **User-user similarity (tuned)** | **1.052** | **0.413** | **0.721** | **0.525** |
| Item-item similarity (baseline) | 1.039 | 0.307 | 0.562 | 0.397 |
| Item-item similarity (tuned) | 1.033 | 0.408 | 0.665 | 0.506 |
| Matrix factorization, SVD (baseline) | 1.025 | 0.410 | 0.633 | 0.498 |
| Matrix factorization, SVD (tuned) | 1.014 | 0.415 | 0.635 | 0.502 |
| Co-clustering (baseline) | 1.049 | 0.397 | 0.582 | 0.472 |
| Co-clustering (tuned) | 1.065 | 0.394 | 0.566 | 0.465 |

The **tuned user-user collaborative filtering model** (Pearson-baseline similarity, k = 30, min_k = 9) had the best F1, so it was chosen as the final model. Tuned SVD had the lowest RMSE, but its recall was lower.

A popularity-based model handles new users who have no listening history. A content-based model (TF-IDF on song title, album and artist text, with cosine similarity) was also built to recommend songs similar to ones a user already likes.

## Next steps

A hybrid system that combines user-user collaborative filtering with matrix factorization or content-based recommendations would likely perform better than any single model, because it draws on several sources of signal.

## Tools

Python, Pandas, NumPy, scikit-learn, Surprise, NLTK, Matplotlib, Seaborn
