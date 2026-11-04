# AI-oglasnik

AI-powered marketplace prototype that turns a user's free-text product description into a structured classified ad.

## Overview

The user enters a short description of an item. Gemini extracts the relevant fields, and the application stores the resulting ad in a local SQLite database for display in the web interface.

Example input:

> Prodajem Samsung S23, 256 GB, očuvan, 450 EUR.

The intended structured fields include title, description, price, and category.

## Technology

- Python
- FastAPI
- Uvicorn
- Google GenAI SDK / Gemini
- Pydantic
- SQLite

## Current prototype capabilities

- Create an ad from free text using AI
- Extract structured ad fields
- Store ads in SQLite
- Display ads through a web interface
- API endpoint to create ads: `POST /oglasi`
- API endpoint to list ads: `GET /oglasi`

## Run locally

The app is intended to run locally. Install the dependencies listed in `requirements.txt`, configure a Gemini API key as required by the application, and start the FastAPI server:

```bash
python -m uvicorn app:app --host 127.0.0.1 --port 8000 --reload
```

Then open `http://127.0.0.1:8000` in your browser.

> Note: This command assumes the application module is named `app.py` and dependencies are listed in `requirements.txt`. Confirm these files and the required environment variable names in the repository before running.

## Planned improvements

- User accounts and authentication
- Edit and delete ads
- Product images
- Search and filters
- Moderation and anti-fraud protections
- Public hosting
- Monetization and promoted listings

## Project status

This repository describes an early prototype, not a production-ready marketplace. Features listed under planned improvements are not claimed to be implemented.

See [`docs/AI-Oglasnik-Dokumentacija.md`](docs/AI-Oglasnik-Dokumentacija.md) for the fuller project documentation.