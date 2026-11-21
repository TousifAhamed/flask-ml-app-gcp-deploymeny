# flask-ml-app-gcp-deploymeny

Flask app (in `BikeShare/`) that predicts bike-share demand with a scikit-learn Random Forest model, packaged for container deployment (e.g. Google Cloud Run / App Engine).

## Run locally (Python 3.11)
```bash
cd BikeShare
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirement.txt
python BikePred.py
```
Open http://localhost:8080.

## Run with Docker
```bash
cd BikeShare
docker build -t bikeshare-gcp .
docker run -p 8080:8080 bikeshare-gcp
```

## Configuration (environment variables)
| Variable | Purpose | Default |
|---|---|---|
| `PORT` | Port the app listens on (Cloud Run sets this automatically) | `8080` |
| `FLASK_DEBUG` | `1` turns on the Flask debugger. **Local development only**: on a reachable server it lets anyone run code. | off |

No API keys or passwords are needed.

## Notes
- The model file `BikeShare/model/bike_share_rf_model.P` was re-saved for scikit-learn 1.5. The original file, pickled with scikit-learn 0.23, can't be loaded by current scikit-learn. The converted model gives **identical predictions**. If you retrain, pickle the model with the same scikit-learn version as in `requirement.txt`.
- The model is loaded relative to `BikePred.py`, so the app runs from any folder or container.
