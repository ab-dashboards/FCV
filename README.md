# FCV Dashboard

FCV is a Streamlit-based dashboard for **semantic retrieval and analysis of project-document corpora**.
It combines embedding search (SentenceTransformer + FAISS) with LLM-assisted summarization to support portfolio-wide and project-wise "distant reading" workflows.

## What this project does

- Embeds and searches document snippets with FAISS.
- Supports faceted filtering by project metadata (country, region, fiscal year, document type).
- Generates:
  - project-wise summaries
  - portfolio-level summaries
  - exploratory visualizations (score histograms, word clouds, scatter plots)
- Includes optional project clustering with KMeans + PCA + LLM-generated cluster themes.

## Repository structure

- `dashboard.py` – lightweight Streamlit dashboard.
- `dashboard_full.py` – full dashboard with faceting and clustering.
- `fcv_query.py` – retrieval + summarization functions used by full dashboard.
- `fcv_query2.py` – retrieval + summarization functions used by lightweight dashboard.

## Quickstart

### 1) Create and activate a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate
```

### 2) Install dependencies

```bash
pip install -r requirements.txt
```

### 3) Configure environment

Copy and edit `.env.example` values (or export env vars directly):

```bash
cp .env.example .env
```

Minimum required variables:

- `FCV_BASE_FOLDER` – directory containing `faiss_index.bin` and `metadata_mapping.pkl`
- `OPENAI_API_KEY` – API key for summarization calls

### 4) Run dashboards

```bash
streamlit run dashboard.py
```

or

```bash
streamlit run dashboard_full.py
```

## Data and provenance

This repository contains dashboard/query code only. The FAISS index and metadata files are expected locally at runtime and are not committed here.

Expected files inside `FCV_BASE_FOLDER`:

- `faiss_index.bin`
- `metadata_mapping.pkl`

## Ethics and responsible use

- Treat source documents as potentially sensitive.
- LLM summarization sends selected snippets to OpenAI APIs.
- Avoid uploading non-public or personally sensitive data unless your usage is compliant with legal and institutional requirements.

## Limitations

- Retrieval quality depends on embedding model + index quality.
- LLM-generated summaries can be incomplete or inaccurate.
- Word clouds are exploratory only and should not be treated as robust statistical evidence.

## License

This project is released under the MIT License (see `LICENSE`).
