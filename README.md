# llm-edge-health-monitoring
An LLM-driven, context-aware framework for real-time multivariate telemetry health monitoring and model orchestration on resource-constrained edge devices.

# Do-Or-Die: LLM-Driven Context-Aware Health Monitoring for Resource-Constrained Edge Devices

[![MDPI Electronics](https://shields.io)](https://mdpi.com)
[![DOI:10.3390/electronics15163579](https://shields.io)](https://doi.org)
[![Zenodo Dataset](https://shields.io)](https://zenodo.org)
[![License: MIT](https://shields.io)](https://github.com/ioatzi/llm-edge-health-monitoring/blob/main/LICENSE)

Official implementation, evaluation configurations, and orchestration pipelines for the **Do-Or-Die** framework, originally published in **MDPI Electronics (Special Issue: Energy Efficient Computer Architecture for Edge Computing)**.

---

## 📑 Citations

### Academic Paper
```bibtex
@Article{electronics15163579,
AUTHOR = {Tzitzios, Ioannis and Dimara, Asimina and Petridou, Georgiana and Kostavelis, Ioannis and Krinidis, Stelios},
TITLE = {{LLM-Driven Context-Aware Health Monitoring for Resource-Constrained Edge Devices}},
JOURNAL = {Electronics},
VOLUME = {15},
YEAR = {2026},
NUMBER = {16},
ARTICLE-NUMBER = {3579},
URL = {https://www.mdpi.com/2079-9292/15/16/3579},
DOI = {10.3390/electronics15163579}
}
```

### Telemetry Dataset
```bibtex
@dataset{tzitzios_2026_zenodo,
  author       = {Tzitzios, Ioannis and Dimara, Asimina and Petridou, Georgiana},
  title        = {{Health Monitoring Raspberry Pi (RPi) Multivariate Telemetry Dataset}},
  month        = jul,
  year         = 2026,
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.20639458},
  url          = {https://zenodo.org/records/20639458}
}
```

---

## 🚀 Framework Architecture

**Do-Or-Die** introduces a novel dual-stage LLM orchestration mechanism that decouples device health state forecasting from resource-aware optimization loops on near-edge configurations.

1. **Stage 1 (Semantic Forecaster):** Analyzes multidimensional device health vectors (\(H_t\)) to estimate semantic health steps (9-levels: `SAFE` to `SOS`) 5 minutes into the future.
2. **Stage 2 (LLM Orchestrator):** Factors in the predicted health state, historical profiles, and user-specified Task Importance Levels (TIL) to dynamically select or toggle candidate local models (`Ridge`, `XGBoost`, `LightGBM`, `CatBoost`) or drop into emergency caching modes.

---

## 🛠️ Repository Layout
```text
├── data/                  # Zenodo processing pipes
│   └── telemetry_raw/     # Dynamic target folder for downloaded CSV records
├── src/
│   ├── sensing/           # vcgencmd, htop, and metric stream collection
│   ├── mapping/           # 9-Level semantic matrix representation parser
│   ├── forecasting/       # Remote Ollama REST client for Stage 1 reasoning
│   ├── orchestrator/      # Task Importance (TIL) handler for Stage 2 switches
│   └── models/            # Native model execution pool (Ridge, XGBoost, CatBoost)
├── scripts/
│   └── download_data.py   # Automated Zenodo API dataset bootstrapper
├── pyproject.toml         # Explicit tool configurations
└── requirements.txt       # Hardened dependency definitions
```

---

## ⚡ Quick Start & Verification

### 1. Project Ingestion
```bash
git clone https://github.com
cd Do-Or-Die-Edge-LLM
pip install -r requirements.txt
```

### 2. Fetch the Zenodo Telemetry Production Dataset
Instead of manually copying data blocks, execute the automated asset collection pipeline to fetch the ~1.3 million historical CSV telemetry rows directly:
```bash
python scripts/download_data.py
```

### 3. Run the Adaptive Orchestration Engine
```bash
python src/main.py --til MEDIUM --llm_endpoint http://YOUR_REMOTE_OLLAMA_IP:11434
```

---

## 📊 Benchmarking & Verification Matrix
The table below showcases the performance improvements of our runtime orchestration model compared to static policies on the Raspberry Pi 5 over a 6-month period, as presented in our paper:

| Strategy | Avg. Accuracy (%) | Avg. CPU (%) | Avg. RAM (%) | Avg. Temp (°C) | Overall Edge Health Status |
| :--- | :---: | :---: | :---: | :---: | :---: |
| *Always Ridge* | 91.8% | 42.3% | 38.5% | 55.8°C | **SAFE** |
| *Always XGBoost* | 95.6% | 81.7% | 73.9% | 77.4°C | **CRITICAL** |
| *Always LightGBM* | 94.9% | 77.8% | 69.4% | 74.6°C | **WARNING** |
| *Always CatBoost* | 95.3% | 79.5% | 71.8% | 76.2°C | **CRITICAL** |
| **Proposed LLM Orchestrator** | **95.4%** | **64.8%** | **56.2%** | **66.5°C** | **SAFE** |

---

## 🤝 Contact & Open-Source Verification
* For questions regarding architectural schemas or system profiles, please open a GitHub Issue or reach out directly to the principal investigators listed in the manuscript.
