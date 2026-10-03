# Real-Time Public Sentiment Dashboard

Tracking public opinion about brands from Twitter/X data using Python, NLTK and Streamlit.

## 📌 Overview
Brands need to know customer feedback in real-time. This project builds an end-to-end pipeline that streams tweets, cleans & classifies sentiment, and visualizes on a live dashboard with daily logs.

Dataset: Twitter US Airline Sentiment (14,640 tweets, 6 airlines - Positive/Negative/Neutral)

## 🛠️ Tech Stack
- **Language:** Python 3, pandas, NumPy
- **Streaming:** Simulated replay (stream_simulator.py), Tweepy StreamingClient
- **NLP:** NLTK (stopwords, WordNet lemmatizer, VADER)
- **ML:** scikit-learn TF-IDF (1-2 grams) + Logistic Regression
- **Dashboard:** Streamlit (auto-refresh), matplotlib

## ⚙️ Pipeline
1. Data collection & class balance check (63% negative, 21% neutral, 16% positive)
2. Cleaning: lowercasing, URL/mention removal, keep negations (not/no/never), lemmatization
3. Baseline: VADER scoring -> 54% accuracy
4. Model Training: TF-IDF + Logistic Regression (80/20 split) -> 77% accuracy
5. Streaming: timestamp -> clean -> classify -> append to `live_tweets.csv`
6. Dashboard: tweet count, sentiment share, net-sentiment KPI, time trend, brand comparison
7. Daily logs: `daily_sentiment.csv` for Tableau / trend tracking

## 📊 Results
| Method | Accuracy | Note |
|---|---|---|
| NLTK VADER (no training) | 54% | Over-predicts positive on complaints |
| TF-IDF + Logistic Regression | 77% | Negative F1 0.85, Neutral F1 0.61 |

Key Learning: General lexicon is not enough for domain-specific sarcasm. Training improved accuracy by 23%.

## 🚀 How to Run
```bash
pip install -r requirements.txt
python stream_simulator.py
streamlit run app.py
