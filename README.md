# Movie Recommender

A small movie recommendation project with a FastAPI backend and a Streamlit frontend. The app combines TMDB data, a local TF-IDF recommender, and genre-based recommendations.

## Features

- Search movies by keyword
- Browse home feeds such as trending, popular, top rated, now playing, and upcoming
- View movie details with poster, backdrop, overview, release date, and genres
- Get two recommendation sets for a selected movie:
  - TF-IDF similarity from the local dataset
  - TMDB genre-based recommendations

## Project Structure

- app.py - Streamlit frontend
- main.py - FastAPI backend
- movies_metadata.csv - source dataset
- requirements.txt - Python dependencies

The backend also expects these generated artifacts in the project root:

- df.pkl
- indices.pkl
- tfidf_matrix.pkl
- tfidf.pkl

## Requirements

- Python 3.10 or newer is recommended
- A TMDB API key
- The pickle artifacts listed above

## Setup

1. Create and activate a virtual environment.
2. Install dependencies:

    pip install -r requirements.txt

3. Create a .env file in the project root with your TMDB key:

    TMDB_API_KEY=your_tmdb_api_key_here

## Run the Backend

Start the FastAPI server first:

    uvicorn main:app --reload --host 0.0.0.0 --port 8000

The backend serves these endpoints:

- GET /health
- GET /
- GET /home
- GET /tmdb/search
- GET /movie/id/{tmdb_id}
- GET /recommend/genre
- GET /recommend/tfidf
- GET /movie/search

## Run the Frontend

In a second terminal, start Streamlit:

    streamlit run app.py

If the backend is running on a different URL, update API_BASE in app.py.

## Notes

- The backend loads the pickle artifacts at startup, so missing files will cause the API to fail on launch.
- The Streamlit app talks to the backend over HTTP, so both processes need to be running for the full experience.
- The TMDB API key is required for search, details, and recommendation endpoints that fetch live poster and movie data.
