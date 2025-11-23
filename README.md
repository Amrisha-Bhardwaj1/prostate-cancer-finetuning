

# 🧠 Prostate Cancer Segmentation — Fine-Tuning Segment Anything (SAM)

This repository contains a full pipeline to **fine-tune the Segment Anything Model (SAM)** on the **PANDA – Prostate Cancer Grade Assessment** dataset.
The objective is to adapt SAM (originally trained on natural images) to perform **medical image segmentation** on prostate histopathology slides.

The project includes:

* 🧬 A complete training pipeline
* ⚙️ Automated checkpointing + interruption-safe saving
* 📁 Config files, logs, and summaries for full reproducibility
* 📊 Loss tracking and visualization
* 📂 Clean, production-ready project structure
* ☁️ Notebook for Colab / Kaggle training

---

## 📂 Project Structure

```
prostate-cancer-finetuning/
│
├── notebook/
│   └── fine_tune_model.ipynb        # Main training notebook
│
├── src/
│   └── utils.py                     # Custom dataset, transforms, helpers
│
├── data/
│   └── .gitkeep                     # Placeholder (dataset not included)
│
├── outputs/
│   ├── backup_epoch1_batch800.pt    # Auto-saved checkpoint  
│   ├── model.pt                     # Final / interrupted model (large file – optional)
│   ├── model_config.yaml            # Auto-generated SAM model config  
│   ├── results_summary.md           # Auto summary of training  
│   ├── training_config.json         # All training hyperparameters  
│   └── training_log.txt             # Full training logs  
│
├── requirements.txt                 # Environment dependencies
├── LICENSE                          # MIT License
└── README.md                        # Project documentation
```

---

## 📊 Dataset Details

### 🧪 Dataset Used

**PANDA – Prostate Cancer Grade Assessment (Resized 512×512)**
📌 Source: [Kaggle Dataset — PANDA Resized](https://www.kaggle.com/datasets/xhlulu/panda-resized-train-data-512x512)

The dataset contains:

* Histopathology slide tiles (512×512)
* Segmentation masks
* Balanced cancer grade distribution

---

## 🔧 Model & Training

### 🧠 Model

* **Base model:** Segment Anything Model (SAM) by Meta AI
* **Fine-tuned variant:** MedSAM / SAM-ViT-B
* **Framework:** PyTorch
* **Training type:** Batch training (batch size = 2)

### 🚀 Training Features

* Automatic **model checkpointing** every N batches
* **Epoch-wise saving** (`model_epoch_X.pt`)
* **KeyboardInterrupt-safe saving** → creates `interrupted_model.pt`
* **Crash-safe saving** → creates `crashed_model.pt`
* Logs saved to:
  ✔ `training_log.txt`
  ✔ `training_config.json`
* Auto-generated:
  ✔ `model_config.yaml`
  ✔ `results_summary.md`

### 📉 Loss Curve

A loss curve (`loss_curve.png`) is generated automatically when training completes.
If interrupted early, you can manually regenerate it using the saved logs.

---

## ⚙️ Installation & Setup

### 1️⃣ Clone the repository

```bash
git clone https://github.com/Amrisha-Bhardwaj1/prostate-cancer-finetuning.git
cd prostate-cancer-finetuning
```

### 2️⃣ Install dependencies

```bash
pip install -r requirements.txt
```

### 3️⃣ Download dataset (Kaggle)

```bash
kaggle datasets download -d xhlulu/panda-resized-train-data-512x512
unzip panda-resized-train-data-512x512.zip -d ./data
```

---

## 🚀 Run the Training

Open notebook:

```bash
jupyter notebook notebook/fine_tune_model.ipynb
```

Or use Google Colab / Kaggle.

The training loop supports:

* Slow GPU environments
* Manual stopping (Ctrl + M → I in Colab)
* Automatic recovery

---

## 🧾 Output Files (Important for Reproducibility)

| File                                | Description                            |
| ----------------------------------- | -------------------------------------- |
| **training_config.json**            | Hyperparameters & environment settings |
| **training_log.txt**                | Per-batch & per-epoch logs             |
| **loss_curve.png**                  | Loss trend over epochs                 |
| **model_config.yaml**               | Model architecture/config dump         |
| **results_summary.md**              | Summary of saved checkpoints           |
| **model.pt / interrupted_model.pt** | Final or interrupted model weights     |
| **backup_epochX_batchY.pt**         | Periodic batch-level checkpoints       |

✔ Push all `.json`, `.txt`, `.png`, `.yaml`, `.md` to GitHub
✔ Model `.pt` files **are optional** because they are large

---

## 🧑‍💻 Author

**Amrisha Bhardwaj**
M.Tech | Computer Science, NIT Bhopal
🔗 GitHub: [https://github.com/Amrisha-Bhardwaj1](https://github.com/Amrisha-Bhardwaj1)

---
