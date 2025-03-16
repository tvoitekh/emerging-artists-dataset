# Emerging Artists Dataset

## Dataset Overview
This dataset contains analytics data for 329 emerging music artists collected from Spotify's API, including popularity metrics, release patterns, playlist presence, and growth indicators.

### Dataset Shape
- Records: 329 rows (artists)
- Features: 24 columns
- Format: CSV

## Data Description

### Features
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| artist_id | string | Unique Spotify identifier for the artist |
| name | string | Artist name |
| followers | integer | Number of followers on Spotify |
| popularity | integer | Spotify popularity score (1-100) |
| genres | list | List of genres associated with the artist |
| total_releases | integer | Total number of releases by the artist |
| releases_last_year | integer | Number of releases in the past year |
| avg_release_interval_days | float | Average number of days between releases |
| days_since_last_release | float | Number of days since the last release |
| playlist_count | integer | Number of playlists the artist appears on |
| sampled_playlists | float | Number of playlists sampled for analysis (up to 10) |
| total_playlist_followers | integer | Total followers across sampled playlists |
| avg_playlist_followers | float | Average followers per playlist |
| total_markets | integer | Number of markets (countries) where the artist is available |
| top_markets | list | List of top 10 markets (country codes) by frequency in releases |
| estimated_monthly_growth_rate | float | Estimated monthly follower growth rate |
| months_since_last_release | float | Number of months since the last release |
| growth_category | integer | Growth category (0=low, 1=medium, 2=high) |
| recency_score | float | Score based on recency of releases (exp(-months_since_last_release/6)) |
| release_velocity | float | Releases per month (releases_last_year / (avg_interval_days/30 + 1)) |
| has_playlists | integer | Binary indicator if artist appears on playlists (0/1) |
| follower_per_release | float | Average followers per release (followers / (total_releases + 1)) |
| popularity_to_follower_ratio | float | Ratio of popularity score to log10(followers) |
| playlist_reach | float | Estimated reach through playlists (total_followers / (playlist_count + 1)) |

## Data Collection Methodology

### Source
Data was collected from the Spotify Web API using the spotipy Python library and direct API requests. The collection process involved:

1. **Artist Discovery**: Initial artist list was compiled from seven curated "emerging artist" playlists:
   - Metal 2025
   - Chill Vibes 
   - Lo-Fi Hip Hop
   - Hits 2025
   - Dance Hits 2025
   - Artists to Watch 2025
   - House Music 2025

2. **Artist Filtering**: Artists were filtered to include only those with fewer than 250,000 followers, focusing on emerging talent.

3. **Data Enrichment**: For each artist, the following data was collected:
   - Basic profile information (name, followers, popularity, genres)
   - Release history and patterns (albums, singles, release dates)
   - Playlist presence and reach (up to 10 sampled playlists)
   - Market availability across global regions

4. **Derived Metrics**: Additional features were calculated including:
   - Release velocity and recency scores
   - Growth estimates based on popularity and recent releases
   - Playlist reach and engagement metrics
   - Follower-to-release ratios

5. **Growth Classification**: A machine learning model (XGBoost classifier) was trained on manually labeled data to categorize artists into growth potential categories (low/medium/high).

## Potential Use Cases
1. Artist growth prediction and talent scouting
2. Playlist impact and promotional strategy analysis
3. Release scheduling optimization
4. Genre-based performance benchmarking
5. Market penetration assessment and targeting

## Data Preparation
The dataset underwent the following preparation steps:
1. Collection of raw metrics from Spotify API
2. Calculation of derived metrics (growth rates, ratios, etc.)
3. Handling of missing values with appropriate defaults
4. Feature engineering based on industry knowledge
5. Growth categorization using machine learning

## Limitations
- Limited visibility into streaming numbers (not available via public API)
- Growth rates are estimates based on proxy signals (popularity, followers, release recency)
- Playlist data is sampled rather than comprehensive (maximum 10 playlists per artist)
- Genre classifications may be incomplete for newer artists
- Market data represents availability rather than performance in those markets
