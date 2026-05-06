# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a personal home directory organized as a `uv` workspace (Python 3.13+). The root `pyproject.toml` declares workspace members; sub-projects are independent Python packages that share a single lockfile (`uv.lock`).

**Workspace members** (from `pyproject.toml`):
- `.` (root `yazeederman` package) — minimal placeholder
- `Documents/projects/langgraph-learning` — LangGraph experiments with Jupyter notebooks

**Other notable sub-projects** (outside the workspace):
- `llm/GPT/` — PyTorch / HuggingFace Transformers scripts (Gemma model via Kaggle)
- `AI/run.py` — Loads Gemma-4 26B from `kagglehub` with `bfloat16` + `device_map="auto"`
- `app/` — Standalone empty Python package skeleton

## Package Manager

All Python work uses [`uv`](https://docs.astral.sh/uv/). Do not use `pip` directly.

```bash
# Run a script in the workspace
uv run main.py

# Add a dependency to a workspace member
uv add <package> --project Documents/projects/langgraph-learning

# Sync all workspace dependencies
uv sync

# Run Jupyter for the langgraph-learning notebooks
uv run --project Documents/projects/langgraph-learning jupyter notebook
```

## LangGraph Learning Project

Located at `Documents/projects/langgraph-learning/`. Dependencies: `langgraph`, `notebook`, `python-dotenv`. The notebook `analysis.ipynb` is the primary working file.

```bash
cd Documents/projects/langgraph-learning
uv run jupyter notebook notebooks/analysis.ipynb
```

## LLM / ML Scripts

- `AI/run.py`: Downloads and runs Google Gemma-4 via `kagglehub` + `transformers`. Requires a Kaggle API key (`~/.kaggle/kaggle.json`) and a GPU with sufficient VRAM.
- `llm/GPT/`: Contains `main.py`, `train.py`, `requirements.txt` — standalone scripts, not part of the uv workspace. Install deps with `pip install -r llm/GPT/requirements.txt` or migrate to uv as needed.
