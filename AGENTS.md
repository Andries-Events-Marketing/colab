# AGENTS.md

## Cursor Cloud specific instructions

This repo is a fork of the Google Gemini cookbook. The "product" is the set of
Jupyter quickstart notebooks under `quickstarts/` (currently
`System_instructions.ipynb`), which demonstrate the Gemini API via the
`google-genai` Python SDK.

### Running / testing the notebooks
- Dependencies (`google-genai`, `jupyter`, `nbconvert`) are installed at the
  system level via the startup update script (`pip --break-system-packages`).
  Console scripts land in `~/.local/bin`, which may not be on `PATH`; invoke
  tools as modules instead, e.g. `python3 -m nbconvert ...`,
  `python3 -m jupyter notebook`.
- There is no lint/build/test suite — validation means executing a notebook
  end-to-end against the live Gemini API.

### Auth caveat (important)
- The notebooks authenticate with `from google.colab import userdata` /
  `userdata.get("GOOGLE_API_KEY")`, which only works inside Google Colab and
  will fail locally. To run locally, supply the key via the environment:
  the `google-genai` SDK reads `GOOGLE_API_KEY` (or `GEMINI_API_KEY`), or pass
  `genai.Client(api_key=...)` explicitly. An API key is available in this
  environment as the secret `GOOGLE_AI_STUDIO_API_KEY` (also
  `GEMINI_AI_API_KEY`). Do NOT edit the committed notebook to change auth; use a
  temporary patched copy for local execution.

### Model caveat
- The notebook's default model `gemini-2.0-flash` is deprecated and returns a
  404. Use a current model such as `gemini-2.5-flash` when running locally.
