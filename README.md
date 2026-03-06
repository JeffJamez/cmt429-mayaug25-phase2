To follow along, update the working directry/path on line 7 to wherever you will download and extract the dataset named "Test2.zip" on you computer.
The "demo.mp4" demostrates the flow of how the analysis works

# 🌿 Plant Disease Classification Using Machine Learning

**Authors:** Wangeci Njiru, Abayo Otieno & Jeff Kigotho

A machine learning pipeline for automated detection and classification of plant leaf diseases using image analysis and multiple classification algorithms implemented in R.

---

## 📋 Overview

This project builds an end-to-end image classification system capable of distinguishing between three plant leaf conditions:

- ✅ **Healthy** — Normal, disease-free leaves
- 🟠 **Powdery Mildew** — Leaves affected by powdery mildew fungal infection
- 🔴 **Rust Disease** — Leaves affected by rust fungal infection

The pipeline covers the full ML workflow: image preprocessing, feature extraction, exploratory data analysis, statistical testing, model training, and performance evaluation across three classification algorithms.

---

## 🔬 Methodology

### 1. Image Preprocessing
- Images loaded from three labelled class folders (`Healthy/`, `Powdery/`, `Rust/`)
- Converted to grayscale and resized to a standard **64×64 pixels**
- Supports `.jpg`, `.jpeg`, `.png`, and `.bmp` formats

### 2. Feature Extraction
19 features are extracted per image across four categories:

| Feature Category | Features |
|---|---|
| **Intensity Statistics** | Mean, std deviation, min, max, range |
| **Texture Features** | Gradient magnitude mean & std (edge detection via Sobel-like filters) |
| **Edge Features** | Edge density (top 20% gradient threshold) |
| **Shape Features** | Symmetry score (horizontal flip correlation) |
| **Histogram Features** | 10 normalised intensity distribution bins |

### 3. Exploratory Data Analysis
- Class distribution analysis
- Per-class feature comparisons (boxplots, scatter plots)
- Feature correlation heatmap
- Disease progression trend analysis (normalised line charts)
- ANOVA-based feature importance ranking

### 4. Statistical Analysis
- **One-way ANOVA** for each key feature across the three classes
- **Tukey's HSD** post-hoc test for pairwise group comparisons
- F-statistics and p-values reported for significance testing

### 5. Machine Learning Models
Three classifiers are trained and evaluated on a **70/30 train-test split**:

| Model | Algorithm |
|---|---|
| Logistic Regression | Multinomial logistic regression with 5-fold cross-validation |
| Decision Tree | CART with minimum split of 10, complexity parameter 0.01 |
| Support Vector Machine | RBF kernel (cost=1, gamma=0.1) |

All features are standardised (zero mean, unit variance) before training.

---

## 📊 Visualisations Generated

The pipeline produces 12 visualisations:

1. Class distribution bar chart
2. Mean intensity boxplot by disease class
3. Texture features boxplot by class
4. Edge density boxplot by class
5. Intensity vs Texture scatter plot
6. Feature correlation heatmap
7. Image brightness histograms (faceted by class)
8. Average leaf characteristics bar chart
9. Brightness vs Texture scatter with regression lines
10. Disease progression line chart (normalised features)
11. Feature usefulness ranking (F-statistic bar chart)
12. Top feature distribution histograms (faceted grid)

Plus model evaluation outputs:
- Model accuracy comparison bar chart
- Decision tree visualisation (rpart.plot)
- Confusion matrix heatmap for the best-performing model

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **R** | Primary programming language |
| **EBImage** | Image loading, resizing, grayscale conversion, filtering |
| **caret** | Model training, cross-validation, preprocessing |
| **e1071** | Support Vector Machine implementation |
| **rpart / rpart.plot** | Decision tree training and visualisation |
| **tidyverse / ggplot2** | Data manipulation and visualisation |
| **caTools** | Train/test split |
| **reshape2** | Data reshaping for heatmap plotting |

---

## 🚀 Getting Started

### Prerequisites

Install required R packages:

```r
install.packages(c(
  "EBImage", "tidyverse", "caret", "e1071",
  "rpart", "rpart.plot", "caTools", "ggplot2",
  "gridExtra", "reshape2"
))

# EBImage is from Bioconductor
if (!requireNamespace("BiocManager", quietly = TRUE))
  install.packages("BiocManager")
BiocManager::install("EBImage")
```

### Dataset Structure

Organise your image dataset in the working directory as follows:

```
project-root/
├── Healthy/
│   ├── image1.jpg
│   ├── image2.jpg
│   └── ...
├── Powdery/
│   ├── image1.jpg
│   └── ...
├── Rust/
│   ├── image1.jpg
│   └── ...
└── plant_disease_classification.R
```

### Running the Pipeline

1. Clone the repository:
```bash
git clone https://github.com/JeffJamez/plant-disease-classification.git
cd plant-disease-classification
```

2. Set your working directory in the script:
```r
setwd("/path/to/your/project")
```

3. Run the full pipeline:
```r
source("plant_disease_classification.R")
```

The script is interactive — press **Enter** to advance through each visualisation.

---

## 📈 Results

Three models are compared on held-out test data:

| Model | Accuracy |
|---|---|
| Logistic Regression | *See output* |
| Decision Tree | *See output* |
| Support Vector Machine | *See output* |

> Accuracy results depend on dataset size and class balance. Run the pipeline with your dataset to see exact figures.

Key diagnostic features identified via ANOVA (ranked by F-statistic):
- **Image Brightness** (mean intensity)
- **Brightness Variation** (std intensity)
- **Texture Roughness** (gradient magnitude)
- **Edge Sharpness** (edge density)

---

## 💾 Output Files

After running the pipeline, the following files are saved to your working directory:

| File | Contents |
|---|---|
| `plant_disease_features.csv` | Full feature matrix with labels |
| `model_performance_summary.csv` | Accuracy comparison across all models |
| `trained_models.rds` | Serialised R model objects for reuse |

---

## 👥 Authors

| Name | Role |
|---|---|
| **Wangeci Njiru** | Co-first author |
| **Abayo Otieno** | Co-first author |
| **Jeff Kigotho** | Co-first author |

---

## 📄 License

This project is open for academic and research use. Please cite the authors if you use this work in your own research.
