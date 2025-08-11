# Evaluating Perceptual Alignment in Vision Transformers for Fashion Sales Prediction

> **TL;DR**  
> Do human-aligned visual embeddings (e.g., from NIGHTS/DreamSim) improve downstream **fashion sales forecasting** compared to vanilla or label-triplet training?  
> This thesis benchmarks multiple vision models and alignment strategies by plugging their embeddings into forecasting models and comparing accuracy.

---

## 📌 Project Status
**In progress** (MSc Thesis, Eberhard Karls Universität Tübingen).  
Planned submission: `<Month October/November>`.

---

## 🌍 Motivation
Retail forecasting for fashion is notoriously hard (new items, short histories, cold-start).  
If perceptual similarity matches human judgment better, embeddings might carry more signal for downstream **demand forecasting**.

---

## 🧩 Research Questions
1. Do **human-aligned** embeddings (NIGHTS → DreamSim-style) improve SKU-level sales forecasts vs. **vanilla** models?  
2. Does **domain-specific human alignment** (fashion triplets) outperform generic human alignment?  
3. Are **label-derived** triplets (no human judgment) a competitive proxy?  
4. How do **fine-tuning strategies** (LoRA vs. standard full fine-tuning) affect results?

---

## 📦 Data
- **Visuelle2** (fashion): images + metadata (e.g., release date, store) + sales series.  
  - Access: `[<link or note about access>](https://humaticslab.github.io/forecasting/visuelle)`.  
  - Preprocessing: image normalization, SKU filtering, time series alignment, train/val/test splits by calendar blocks.  
- **Triplet sources**  
  - **NIGHTS** (human similarity judgments).  
  - **Fashion-triplets (small, in-domain)** — collected by `<our team / collaborators>` (much smaller than NIGHTS).  
  - **Label-triplets** — automatically generated from categorical attributes (e.g., two *red dresses* vs. *red dress* vs. *blue jeans*).

> ⚖️ **Ethics & Licensing**: Use NIGHTS and Visuelle2 under their respective licenses; ensure proper attribution and non-commercial restrictions if any.

---

## 🔬 Methods Overview

### Vision backbones & alignment variants
- **Backbones**: ViTs (primary). *(Optional/Appendix: CNNs if included)*  
- **Variants compared**:
  1) **Vanilla** (pretrained, no extra alignment)  
  2) **NIGHTS-aligned** (DreamSim-style objectives; DINO/CLIP/OpenCLIP family)  
  3) **Fashion human-triplets** (small, domain-specific)  
  4) **NIGHTS + Fashion** (combined)  
  5) **Label-triplets** (no human judgments)

### Fine-tuning strategies
- **LoRA** adapters  
- **Full/standard fine-tuning** (MLE-style objectives)

### Forecasting models (consume embeddings)
- Classical + ML: `<XGBoost / LightGBM / RandomForest>`  
- Deep/time-series: `<TFT / TCN / simple LSTM / Prophet as baseline>`  
- Hierarchy or group handling: `<by store / item / category>` (if applicable)

### Evaluation
- Metrics: **MAPE, WAPE, MAE, SMAPE** (+ **CRPS** if probabilistic)  
- Robustness: rolling-origin splits; new-item (cold-start) slices; category/store segmentation  
- Statistical tests: `<Diebold–Mariano / permutation tests>` where relevant

---

## 🗂️ Repository Structure
