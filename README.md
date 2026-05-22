# ML-Driven-Social-Welfare-Scheme-Recommendation-System
Predicts NSAP scheme code (`IGNDPS`, `IGNOAPS`, `IGNWPS`) from district-level beneficiary data.

---

## Files & What They Do

| File | Purpose |
|---|---|
| `train.py` | Trains the model, saves it to `models/` |
| `app.py` | Flask server — loads model, serves UI and API |
| `templates/index.html` | Web UI — must stay inside `templates/` folder |
| `requirements.txt` | Python packages |
| `render.yaml` | Render.com deploy config only |

---

## Run Order (Never Change This)

```
1. pip install -r requirements.txt
2. python train.py        ← must run first, creates models/
3. python app.py          ← start server AFTER train.py
```

---

## Things That Must NOT Be Changed

- `templates/` folder name — Flask looks for this exact folder name
- Feature names in `app.py` must exactly match column names in the CSV
- Ratio features engineered in `train.py` must be identically re-engineered in `app.py`
- `models/best_pipeline.joblib` and `models/label_encoder.joblib` — filenames are hardcoded in `app.py`
- Target column name is `schemecode` — hardcoded in `train.py`
- `data/nsapallschemes.csv` path — set via `DATA_PATH` env variable or defaults to `data/`

---

## Input Features (12 columns required)

```
lgdstatecode, lgddistrictcode,
totalbeneficiaries, totalmale, totalfemale, totaltransgender,
totalsc, totalst, totalgen, totalobc,
totalaadhaar, totalmobilenumber
```

---

## API

`POST /predict` — send above 12 fields as JSON, get back prediction + probabilities  
`GET /health` — check if server is running

---

## .gitignore (Required)

```
models/
__pycache__/
*.pyc
.env
.DS_Store
```

