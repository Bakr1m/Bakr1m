# Abdelkarim Khayi — ML Engineer

End-to-end ML systems: dataset → model → evaluation → API → Docker →
Kubernetes. Healthcare AI + Earth Observation. Every production repo ships
source + hermetic tests + model card + CI/CD, serves a release-pinned
artifact (SHA256-verified), and can be tried in 60 seconds from a
prebuilt image. Every model is evaluated with the metric its business
problem demands — and every README documents what broke along the way.

## Production systems

| Project | Problem | Approach | Key result | Try it |
|---|---|---|---|---|
| [Hospital Readmission Risk](https://github.com/Bakr1m/hospital-readmission-risk-predictor) | Flag 30-day readmissions at discharge | LightGBM + SHAP, cost-tuned threshold | ROC-AUC 0.689, $4.45M cost-optimal | `bakr1m/readmission-api:latest` · :8001 |
| [Sepsis Early-Warning](https://github.com/Bakr1m/sepsis-early-warning) | Score deterioration hourly, 6h ahead | Causal windows + LightGBM vs LSTM, replay simulator | ROC-AUC 0.75, alert-load quantified | `bakr1m/sepsis-api:latest` · :8002 |
| [Chest X-Ray Pneumonia](https://github.com/Bakr1m/chest-xray-pneumonia-detector) | Triage radiology queue | MobileNetV2 transfer + Grad-CAM, offline-safe image | ROC-AUC 0.962, recall 0.99 | `bakr1m/pneumonia-api:latest` · :8003 |
| [Clinical Document RAG](https://github.com/Bakr1m/clinical-document-rag) | Query clinical notes in natural language | FAISS + refusal contract + verified citations | hit-rate 13/15, 11/17 graded | `bakr1m/rag-api:latest` · :8004 |
| [Patient No-Show Optimizer](https://github.com/Bakr1m/noshow-optimizer) | Cut missed appointments | Cost-tuned XGBoost + reminder simulation | $178k / 26% saved in simulation | `bakr1m/noshow-api:latest` · :8005 |
| [Titanic Survival Prediction](https://github.com/Bakr1m/Titanic_Survival_prediction) | Foundations capstone: full lifecycle on a small, understood dataset | sklearn pipelines, leak-free serving contract | ROC-AUC 0.8435 | `bakr1m/titanic-api:latest` · :8006 |
| [EuroSAT Land-Use CNN](https://github.com/Bakr1m/eurosat-landuse-cnn) | Automate satellite land-cover mapping (thesis, productionized) | Custom 3-block CNN, independent rerun | Test accuracy 0.8763 | `bakr1m/eurosat-api:latest` · :8007 |

```bash
docker run -d -p 8001:8000 bakr1m/readmission-api:latest  # or any image above
curl http://localhost:8001/health
# each README has a 60-second block with a verified predict example
```

Pneumonia and EuroSAT also run on Kubernetes: digest-pinned manifests in
each repo's `k8s/`, validated on a local `kind` cluster (probes + live
predictions in-cluster).

## Research studies

| Project | Question | Honest result |
|---|---|---|
| [MAGIC Gamma-Telescope Classifier](https://github.com/Bakr1m/magic-gamma-telescope) | Which model family separates gamma showers from hadron background? | MLP 0.8754 acc — after fixing the scaler leakage + unstratified split in the original analysis. pytest + CI, no serving by design. |

## How these are built

- **Hermetic tests**: pass with real data and with synthetic fallbacks — CI
  has no `data/` by design. Import-time artifact loads are banned; models
  load lazily, missing artifacts fail as request-time errors.
- **Release-pinned artifacts**: Dockerfiles fetch models by exact release
  tag and verify SHA256 at build time — never a moving tag, never baked
  from a laptop.
- **CI/CD**: tests gate every Docker build; each push publishes `:latest` +
  an immutable `:<sha>` tag and smoke-tests the shipped image
  (`/health` + a real prediction).
- **Documented failures**: each README has a *Problems Encountered* section
  — hidden downloads, leaky schemas, alert fatigue, metric gaps between
  reported and reproduced. Bugs found, fixed, and written down.

Stack: Python · scikit-learn · XGBoost/LightGBM · PyTorch + TensorFlow
(CPU) · FastAPI · Docker · Kubernetes (kind) · MLflow · FAISS ·
SHAP/Grad-CAM · pytest + ruff + GitHub Actions.
