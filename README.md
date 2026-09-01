# Social Media Analytics Project
## Milan-Cortina 2026 Winter Olympics
Analysis of sentiment and social network dynamics on Reddit in the lead-up to the Milan-Cortina 2026 Winter Olympic Games.

## Overview
This project analyzes the online discourse around the **Milan-Cortina 2026 Winter Olympics** on Reddit, combining three complementary analytical dimensions:

- **Sentiment Analysis**:  measuring the emotional tone of comments across sport-specific subreddits using VADER and RoBERTa
- **Named Entity Recognition (NER)**: identifying the most frequently mentioned athletes, nations, organizations, and events
- **Social Network Analysis (SNA)**: mapping user interaction networks to detect influence hubs and thematic communities

## Data
Data was collected via **Arctic Shift**, a public API for querying Reddit's historical archive.

| Parameter | Value |
|---|---|
| Posts collected | 908 |
| Total comments | 24,745 |
| Unique authors | 9,355 |
| User-to-user interactions | 20,691 |
| Subreddits | olympics, FigureSkating, hockey, biathlon, Curling, skiing, snowboarding |
| Period covered | Late December 2024 – Late March 2025 |
| NER sample | 8,000 comments (stratified random sample) |

Collection was performed in two phases: post retrieval by keyword, followed by paginated comment download for each post. Deleted and empty comments were excluded.

## Models

### Sentiment Analysis

- **VADER**: rule-based lexical model optimized for social media text; applied to the full corpus of 24,745 comments. Returns a compound score in `[-1, +1]`.
- **RoBERTa** (`cardiffnlp/twitter-roberta-base-sentiment`): transformer fine-tuned on Twitter data for three-class classification (positive / neutral / negative). Applied to a subset for comparison with VADER.

### Named Entity Recognition

- **spaCy** `en_core_web_sm`  applied to a random sample of 8,000 comments. Entity types: `PERSON`, `GPE`, `ORG`, `EVENT`, `LOC`.

### Social Network Analysis

The interaction graph was constructed from parent-child comment relationships. Metrics computed:

- **In-degree centrality**: number of replies received (popularity)
- **PageRank**: quality-weighted influence measure
- **Community detection**: Greedy Modularity Optimization on the undirected graph

Analysis was conducted on a filtered subgraph of users with ≥ 5 interactions (690 nodes, 2,571 edges).

## Key Results

- **Global sentiment**: 55% positive, 24% neutral, 21% negative (avg. VADER compound = +0.24)
- **Most positive subreddit**: r/biathlon (62% positive, avg. VADER = 0.31)
- **Most critical subreddit**: r/skiing (34% negative, avg. VADER = 0.09)
- **VADER vs. RoBERTa agreement**: 57.6% overall; highest for the positive class (88%)
- **Most mentioned athlete**: Alysa Liu (~100 mentions), followed by Kaori Sakamoto and Ami Sato
- **Most mentioned country**: Canada (~270 mentions), followed by Italy and the USA
- **Network structure**: 74 communities detected; strong subreddit-to-community correspondence, suggesting thematic echo chambers

## Project Structure

```
.
├── Data/                                # Datasets
│   ├── reddit_raw.csv
│   ├── reddit_comments.csv
│   ├── reddit_comments_sentiment.csv
│   ├── ner_entities.csv
│   ├── centrality_measures.csv
│   ├── community_partition.csv
│   ├── network_communities.csv
│   └── reddit_network_edges.csv
├── Notebooks/                           # Notebook 
│   ├── Data Searching and loading.ipynb
│   ├── SMA_olympycs_sentiment.ipynb
│   ├── Sma_03_ner_sentiment_tempo.ipynb
│   └── Social_Network_Analysis.ipynb
├── Visualizations/                      # Images and plots
├── Report/                              # Final report
├── Presentations/                       # presentation .pptx
└── README.md
```


## Authors
Davide Fabio Loreti - 865309

Carlo Pegoraro - 865329


