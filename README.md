# Digitization of hydrological variables

This repository contains **Jupyter notebooks** that turn **hydrological charts** (for example GIF animations of flow over time) into **structured tables**, using large language models. The goal is to recover numeric time series and related labels from images so they can be checked, compared, and saved as spreadsheets.

## What is inside

| Area | Contents |
|------|----------|
| `Gemini/` | `gemini_results.ipynb` — Google **Gemini** pipeline with step-by-step phases (setup, API config, batch processing). Reads chart GIFs from `test_pictures/`. |
| `claude/` | `HydrologyClaude.ipynb` — **Anthropic Claude** experiments on the same kind of material. |
| `claude_chain/` | `hydrologyclaudechain.ipynb` — first “chain” style Claude workflow. |
| `claude_chain2/` | `hydrologyclaudechain2.ipynb` — evolved chain workflow. | the most stable one
| `claude_chain3/` | `hydrologyclaudechain3.ipynb` — further iteration of the chain approach. |
| `claude_chain2 base/` | Earlier bulk run: **Excel outputs**, **reformatted** tables, **mismatch** debugging sheets, and **accuracy** summaries for many Italian station-style files. Useful as reference outputs, not the primary entry point for new runs. |
| `test_pictures/` | Sample **GIF** (and related) inputs used by the notebooks. |

There is no separate Python package here; everything runs through the notebooks, which install their own dependencies where needed.

## Requirements

- **Python 3** and **Jupyter** (or VS Code / Cursor with a notebook kernel).
- **API keys** for the providers you use:
  - **Gemini** (`Gemini/gemini_results.ipynb`): a Google AI Studio key ([get a key](https://aistudio.google.com/apikey)).
  - **Claude** (all other notebooks listed above): an **Anthropic** API key.

## Configuration

1. Copy `.env.example` to `.env` in the **project root** (the same folder as `.gitignore`).
2. Set your secrets in `.env` (this file is **not** committed):
   - `GEMINI_API_KEY=` — for the Gemini notebook.
   - `ANTHROPIC_API_KEY=` — for the Claude notebooks.
3. Optional for Gemini: `GEMINI_MODEL=` (default in the notebook is `gemini-2.0-flash` if unset).

Claude notebooks load environment variables with `python-dotenv` from your working directory; run Jupyter from the **repo root** so `.env` is found reliably.

## How to run

1. Create a virtual environment if you like (for example `.venv/` — already ignored by git).
2. Open the notebook you need and run cells **from the top**, in order. The first cells usually install packages (`pip install …`) and set paths.
3. For `Gemini/gemini_results.ipynb`, follow the **Phase 1 → Phase 2 → …** structure in the markdown cells; Phase 1 only checks paths and loads the key without calling the API.

## Note on data

Sample images and spreadsheets are for **research and testing**. Check licensing and privacy before applying this to new datasets.
