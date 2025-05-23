# Music-Recommendation-System

## 🎵 **Thought Process Behind the Music Recommendation System Project**

---

### 🔍 **1. Problem Statement**

> *"How can we recommend music to users based on their tastes, even when we don’t have their listening history?"*

Most real-world platforms use collaborative filtering (based on user interactions), but in cold-start cases (new users/songs), we can use **audio content** itself.

---

### 📁 **2. Data Collection & Understanding**

You started with **three datasets**:

| Dataset | What It Contains | Use Case |
|--------|------------------|----------|
| `data` (170k songs) | Individual tracks with detailed audio features + popularity | Core dataset for clustering and recommendation |
| `genre_data` (2.9k) | Averaged features for each genre | Used to understand genre-wise similarity |
| `test_data` (100) | Small sample set | Possibly for testing the recommender |

You explored each dataset's features — things like:
- `danceability`, `energy`, `valence` (emotion)
- `tempo`, `duration_ms`, `loudness`, `key`, etc.

---

### 🧼 **3. Preprocessing & Feature Selection**

You focused only on **numerical features**, scaled them using `StandardScaler`, and stored the list of relevant columns (`number_cols`).

Why?
> To make different features (like tempo and loudness) comparable — scaling is essential before clustering or similarity analysis.

---

### 🎯 **4. Clustering (Genre-Level and Song-Level)**

You did **unsupervised learning** to discover natural groupings:

#### ✅ Genre-Level Clustering
- Used `KMeans(n_clusters=10)` on `genre_data`.
- Then visualized using `t-SNE` for 2D embedding.
- Found out how genres relate to each other.

#### ✅ Song-Level Clustering
- Used `KMeans(n_clusters=20)` on full song dataset.
- Visualized using `PCA` (faster than t-SNE for large data).
- Helped understand which songs are similar at the **track level**, not just genre.

Why?
> This sets the foundation for later recommendations — songs in the same cluster likely "feel" similar.

---

### 🧠 **5. Building the Recommendation Engine**

You created a content-based recommender using:
- **Cosine similarity** between songs.
- Fallback to **Spotify API** when a user song isn’t in the dataset.

#### Process:
1. User provides song(s).
2. You fetch each song’s audio features from dataset or Spotify.
3. Compute a **mean vector** = average sound profile of those songs.
4. Compare that to your full dataset.
5. Return the **closest songs** based on cosine similarity.

---

### 📊 **6. Visualization**

Using `plotly`, you made:
- Interactive scatter plots of clusters.
- Hoverable titles to make sense of what songs are in each cluster.

Why?
> This makes your work more **intuitive and explainable** to users or stakeholders.

---

## 🚀 The Outcome

You’ve built a powerful **content-based music recommendation engine** that:
- Works with or without Spotify API support.
- Can visualize and explore the music space.
- Doesn't rely on user history or interactions.
- Finds sonically similar tracks based on actual audio properties.

# VERSION--2



# 🎵 Mood-Based and Content-Aware Music Recommendation System

This project is a comprehensive **Music Recommendation System** that leverages both unsupervised learning and external Spotify API integration to provide tailored music suggestions. It supports two key recommendation approaches:
1. **Content-Based Filtering** using audio features
2. **Mood-Based Recommendation** for different emotional contexts

---

## 📊 Features & Technologies

- Clustering using **K-Means** on audio features
- Dimensionality reduction with **PCA** and **t-SNE**
- Interactive visualization using **Plotly**
- **Spotify API** for fetching song metadata and audio features
- **Custom mood profiles** for emotional or situational music discovery
- Cosine and Euclidean distance-based recommendation system

---

## 🛠 How It Works

1. **Data Processing**
   - Loads datasets (`data.csv`, `data_by_genres.csv`, `data_by_year.csv`)
   - Standardizes and clusters songs using K-Means

2. **Visualization**
   - Plots 2D embeddings using **t-SNE** and **PCA** for genre and song clusters

3. **Recommendation Engine**
   - Finds songs similar to a given list by calculating audio feature distances
   - Offers mood-specific suggestions using predefined emotional vectors

4. **Spotify Integration**
   - Searches for new songs using Spotify's Web API
   - Fetches detailed features to recommend even if songs are not in the dataset

---

## 🤖 Use Cases

- Discover music similar to your favorite tracks
- Get playlist suggestions for moods like *party*, *chill*, *romantic*, *focus*, etc.
- Analyze audio trends across genres and years

---

## 🚀 Future Improvements

- Deploy as a web app using Streamlit or Flask
- Add collaborative filtering with user listening history
- Store user interactions and preferences

---

## 📎 Dataset Sources

- Kaggle (Spotify audio features dataset)
- Spotify Web API

---


