# ML Engineer (Healthcare AI)

5 end-to-end ML projects: dataset → model → evaluation → API → Docker →
deployment. Every repo ships source + tests + README + deploy instructions,
and every model is evaluated with the metric its business problem demands.

| # | Project | Business problem | Approach | Key result |
|---|---|---|---|---|
| 1 | [Hospital Readmission Risk](https://github.com/Bakr1m/hospital-readmission-risk-predictor) | Flag 30-day readmissions at discharge | LightGBM + SHAP, cost-tuned threshold | ROC-AUC 0.689, cost-optimal recall |
| 2 | [Sepsis Early-Warning](https://github.com/Bakr1m/sepsis-early-warning) | Score deterioration hourly, 6h ahead | Causal windows + LightGBM vs LSTM, replay simulator | ROC-AUC 0.75, alert-load quantified |
| 3 | [Chest X-Ray Pneumonia](https://github.com/Bakr1m/chest-xray-pneumonia-detector) | Triage radiology queue | MobileNetV2 transfer + Grad-CAM | ROC-AUC 0.962, recall 0.99 |
| 4 | [Clinical Document RAG](https://github.com/Bakr1m/clinical-document-rag) | Query clinical notes in natural language | FAISS + refusal contract + verified citations | hit-rate 13/15, 11/17 graded |
| 5 | [Patient No-Show Optimizer](https://github.com/Bakr1m/noshow-optimizer) | Cut missed appointments | Cost-tuned XGBoost + reminder simulation | $178k / 26% saved in simulation |

DockerHub images: `bakr1m/readmission-api`, `bakr1m/sepsis-api`,
`bakr1m/pneumonia-api`, `bakr1m/rag-api`, `bakr1m/noshow-api` (all `:v1`).

Stack: Python · scikit-learn · XGBoost/LightGBM · PyTorch (CPU) · FastAPI ·
Docker · MLflow · FAISS · SHAP/Grad-CAM · pytest + ruff + GitHub Actions.
