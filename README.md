# Exoplanet Explorer: CWS Project Submission

**Name:** Harshal Sonune
**Enrolment No.:** 24123041 (Engineering Physics)
**Course:** PHC-351 Fundamentals of AI/ML, Dept. of Physics, IIT Roorkee

## Contents

| Template item | Location |
|---|---|
| 3.1 Zip of all code files and libraries | `Exoplanet_Explorer_code.zip` (libraries listed in `requirements.txt` inside) |
| 3.2 Training data | `training data/` |
| 3.3 Testing data | `testing data/` |
| 3.4 PowerPoint | `presentation/Exoplanet_Explorer.pptx` (+ PDF copy) |
| 3.5 VideoPPT | `VideoPPT/` (speaking script included; video to be added) |
| 3.6 Pre-print article | `article/` |

### Training data
* `exoTrain_real_kepler.csv`: real Kepler/K2 light curves (Kaggle "Kepler Labelled Time Series Data"), 5,087 stars, 37 planets. Used to train `models/exoplanet_model_real.keras`.
* `exoTrain_simulated.csv`: simulated light curves used for the older simulated-data model.

### Testing data
* `exoTest_real_kepler.csv`: held-out real Kepler/K2 test set, 570 stars, 5 planets. Used once, for the final results.
* `sample_stars_simulated.csv`: 12 simulated demo stars for trying the web app.
* `spectra/`: 4 simulated transmission spectra for the Molecular Composition tab.

## How to run

```bash
unzip Exoplanet_Explorer_code.zip && cd Exoplanet_Explorer_code
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp "../training data/exoTrain_real_kepler.csv" data/real/exoTrain.csv
cp "../testing data/exoTest_real_kepler.csv"   data/real/exoTest.csv
pytest                      # 66 tests
uvicorn app:app             # open http://127.0.0.1:8000
```

## Main results (real Kepler data)

| | Held-out test (570 stars, 5 planets) | 5-fold CV (5,657 stars, 42 planets) |
|---|---|---|
| ROC AUC | 0.959 | 0.794 ± 0.086 |
| Average precision | 0.394 (random 0.009) | 0.213 ± 0.109 |
| Planets found at 0.5 | 2 of 5 | 8 of 42 (19%) |
| False alarms | 2 of 565 | 19 of 5,615 |

Vetting stage (7,328 real Kepler KOIs, tested on 1,927 unseen stars): rejects 77.3% of false positives and keeps 89.1% of planets.

This research has made use of the NASA Exoplanet Archive, which is operated by the California Institute of Technology, under contract with the National Aeronautics and Space Administration under the Exoplanet Exploration Program.
