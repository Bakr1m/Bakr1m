# Hi there 👋

I am Abdelkarim, everyone calls me Karim. AI is my enthusiasm, building trustworthy and scalable systems that turns data into better decisions is my headline.
Please, feel free to test my products, each is explained and shippable in 60 seconds from a prebuilt image.


- 💼 [LinkedIn — in/abdelkarimkhayi](https://www.linkedin.com/in/abdelkarimkhayi)
- 🐦 [X — @AbdelkarimKhayi](https://x.com/AbdelkarimKhayi)
- 📂 Start with the [Core 3](#-core-3--start-here) each runs in 60 seconds.

> **Open to:** Applied ML / AI Engineer roles (GenAI, healthcare, ML systems). I work AI-assisted (OpenCode/Claude) with rigorous review: green CI, hermetic tests, and documented failures on every repo.

## 🤖 Why my work is different

- **Business first, metrics second.** No-show threshold tuned at $150 miss vs $5 false alarm → $178k saved. Readmission threshold tuned to cost, not 0.5 → $4.45M cost-optimal.
- **GenAI with guardrails.** RAG over 80 clinical notes that *refuses* when evidence is weak and cites exact chunk IDs — retrieval graded 8/10 *before* generation existed.
- **Explainability built in.** SHAP for tabular, Grad-CAM overlays for X-rays — every prediction ships its reason, not just a score.
- **Honest engineering.** Each README has *Problems Encountered*: leaky schemas, SMS confounding, unusable val splits, border-attending FPs. Bugs found, fixed, written down.

## ⭐ Core 3 — start here

### 1. [Clinical Document RAG](https://github.com/Bakr1m/clinical-document-rag)  —>  my differentiator
Clinicians drown in notes. This answers natural-language questions over 80 clinical documents with verified citations — and says `NOT FOUND IN THE PROVIDED NOTES` when evidence is weak.
`FAISS + refusal contract · hit-rate 13/15, 11/17 graded` · `bakr1m/rag-api:latest`

### 2. [Patient No-Show Optimizer](https://github.com/Bakr1m/noshow-optimizer)  —> money story
Missed appointments burn clinician time. Cost-tuned XGBoost + reminder simulation on 110k appointments.
`XGBoost ROC-AUC 0.734 · $178k / 26% saved` · `bakr1m/noshow-api:latest`

### 3. [Chest X-Ray Pneumonia Detector](https://github.com/Bakr1m/chest-xray-pneumonia-detector)  —> strongest metric
Radiology triage support: flag likely pneumonia for prioritized review. Decision support only — never autonomous diagnosis.
`MobileNetV2 fine-tuned · ROC-AUC 0.962, recall 0.99 (4 misses / 390)` · `bakr1m/pneumonia-api:latest`

## All production systems

| Project | Problem | Approach | Key result | Try it |
|---|---|---|---|---|
| [Chest X-Ray Pneumonia](https://github.com/Bakr1m/chest-xray-pneumonia-detector) ⭐ | Triage radiology queue | MobileNetV2 transfer + Grad-CAM, offline-safe image | ROC-AUC 0.962, recall 0.99 | `bakr1m/pneumonia-api:latest` · :8003 |
| [Clinical Document RAG](https://github.com/Bakr1m/clinical-document-rag) ⭐ | Query clinical notes in natural language | FAISS + refusal contract + verified citations | hit-rate 13/15, 11/17 graded | `bakr1m/rag-api:latest` · :8004 |
| [Patient No-Show Optimizer](https://github.com/Bakr1m/noshow-optimizer) ⭐ | Cut missed appointments | Cost-tuned XGBoost + reminder simulation | $178k / 26% saved in simulation | `bakr1m/noshow-api:latest` · :8005 |
| [Hospital Readmission Risk](https://github.com/Bakr1m/hospital-readmission-risk-predictor) | Flag 30-day readmissions at discharge | LightGBM + SHAP, cost-tuned threshold | ROC-AUC 0.689, $4.45M cost-optimal | `bakr1m/readmission-api:latest` · :8001 |
| [Sepsis Early-Warning](https://github.com/Bakr1m/sepsis-early-warning) | Score deterioration hourly, 6h ahead | Causal windows + LightGBM vs LSTM, replay simulator | ROC-AUC 0.75, alert-load quantified | `bakr1m/sepsis-api:latest` · :8002 |
| [EuroSAT Land-Use CNN](https://github.com/Bakr1m/eurosat-landuse-cnn) | Automate satellite mapping (thesis, productionized) | Custom 3-block CNN, independent rerun | Test accuracy 0.8763 | `bakr1m/eurosat-api:latest` · :8007 |
| [Titanic Survival](https://github.com/Bakr1m/Titanic_Survival_prediction) | Foundations capstone | sklearn pipelines, leak-free serving contract | ROC-AUC 0.8435 | `bakr1m/titanic-api:latest` · :8006 |

```bash
docker run -d -p 8003:8000 bakr1m/pneumonia-api:latest  # or any image above
curl http://localhost:8003/health
# each README has a 60-second block with a verified predict example
```

Pneumonia and EuroSAT also run on Kubernetes: digest-pinned manifests in each repo's `k8s/`, validated on a local `kind` cluster (probes + live predictions in-cluster).

## Research

| Project | Question | Honest result |
|---|---|---|
| [MAGIC Gamma-Telescope Classifier](https://github.com/Bakr1m/magic-gamma-telescope) | Which model family separates gamma showers from hadron background? | MLP 0.8754 acc — after fixing the scaler leakage + unstratified split in the original analysis. pytest + CI, no serving by design. |

## How I build trustworthy systems

- **Hermetic tests**: pass with real data and with synthetic fallbacks — CI has no `data/` by design. Import-time artifact loads are banned; models load lazily, missing artifacts fail as request-time errors.
- **Release-pinned artifacts**: Dockerfiles fetch models by exact release tag and verify SHA256 at build time — never a moving tag, never baked from a laptop.
- **CI/CD**: tests gate every Docker build; each push publishes `:latest` + an immutable `:<sha>` tag and smoke-tests the shipped image (`/health` + a real prediction). **8/8 repos green.**
- **Documented failures**: each README has a *Problems Encountered* section — hidden downloads, leaky schemas, alert fatigue, metric gaps between reported and reproduced. Bugs found, fixed, and written down.

**What I won't claim:** retrospective ≠ prospective. Single-site data ≠ generalizable. Similarity scores ≠ calibrated probabilities. Every repo states its limits up front.

Stack: Python · scikit-learn · XGBoost/LightGBM · PyTorch + TensorFlow (CPU) · FastAPI · Docker · Kubernetes (kind) · MLflow · FAISS · SHAP/Grad-CAM · pytest + ruff + GitHub Actions.

