# SimurG — Turkish NER & Entity-Centric Sentiment API

**Short:**  
SimurG extracts `ORG` entities (including `@mentions`) from Turkish text and performs entity-centric sentiment analysis on a short right-side context. Provides a FastAPI JSON endpoint.

## Features
- Turkish NER (Hugging Face token-classification)
- Treats `@mentions` as `ORG`
- Sentiment analysis on a configurable right-side context window
- Simple POST `/predict/` endpoint returning JSON

## Models (changeable)
- NER: `korkmazemin1/Named_entity_recognition_turkish_simurg`  
- Sentiment: `korkmazemin1/sentiment_analys_turkish_simurg`

## Requirements
- Python 3.9+  
- Packages: `fastapi`, `uvicorn[standard]`, `transformers`, `torch`, `pydantic`, `python-dotenv`

Example `requirements.txt`:
```
fastapi
uvicorn[standard]
transformers
torch
pydantic
python-dotenv
```

## Quick install (local)
```bash
git clone https://github.com/<you>/simurg.git
cd simurg
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
export HUGGINGFACE_TOKEN="hf_xxx"   # optional
uvicorn upwork_try:app --host 127.0.0.1 --port 7444 --reload
```

## API
- `GET /` — simple demo page  
- `POST /predict/` — JSON body: `{"text":"..."}`

Example curl:
```bash
curl -X POST "http://127.0.0.1:7444/predict/" -H "Content-Type: application/json" -d '{"text":"Hello @Turkcell I have a speed issue, SuperOnline 100mb problem..."}'
```

Example response:
```json
{
  "entity_list": ["@Turkcell", "SuperOnline"],
  "results": [
    {"entity": "@Turkcell", "sentiment": "negative"},
    {"entity": "SuperOnline", "sentiment": "neutral"}
  ]
}
```

## Configuration
- `ner_model_name`, `sentiment_model_name` (in code)  
- `context_window_size` — right-context length (e.g., 10)

## Notes
- For production: use a process manager, pin model versions, and consider batching/model servers.  
- Use `HUGGINGFACE_TOKEN` for private models.

## License & Contact
- Suggested license: MIT  
- Add name / email / GitHub as needed.



# DATASET

To download dataset click [here.](https://drive.google.com/drive/folders/1me_JE582N-Wwpdx-nX4kYcZAOgyIvtvg?usp=sharing)
