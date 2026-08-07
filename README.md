<div align="center">

# 🛡️ AI-Driven Phishing Email Detection

### Classifying phishing vs. legitimate emails using NLP + Machine Learning

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)](https://scikit-learn.org)
[![NLTK](https://img.shields.io/badge/NLTK-NLP-3776AB?style=flat-square)](https://www.nltk.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)](https://jupyter.org)
[![Best Accuracy](https://img.shields.io/badge/Best%20Accuracy-98.28%25-brightgreen?style=flat-square)](#-results)

An end-to-end ML pipeline that cleans raw email text, extracts TF-IDF features, and benchmarks four classification algorithms to flag phishing emails with **98%+ accuracy**.

</div>

---

## 📋 Overview

This project builds and compares multiple machine learning classifiers to automatically detect phishing emails using **Natural Language Processing**. Raw email text is cleaned and normalized, converted into TF-IDF feature vectors, and fed into four different models — with the best-performing one selected based on accuracy, precision, recall, and F1-score.

The entire workflow — from raw data to trained, serialized models — is documented step-by-step in a single Jupyter notebook.

## ✨ Highlights

- 🧹 **Full text preprocessing pipeline** — lowercasing, URL/HTML stripping, digit removal, punctuation removal, stopword filtering
- 🔢 **TF-IDF feature extraction** with a 5,000-feature vocabulary
- 🤖 **Four models trained & benchmarked** on identical train/test splits for fair comparison
- 📊 **Full evaluation suite** — accuracy, precision, recall, F1-score, and confusion matrices for every model
- 💾 **Ready-to-use trained models** shipped as `.pkl` files — no retraining required to run predictions
- 📄 **Written project report** included as a PDF

## 🧠 How It Works

```
Raw Email Text
      │
      ▼
┌─────────────────────┐   lowercase → strip URLs/HTML → remove digits &
│  Text Preprocessing │   punctuation → remove stopwords
└─────────────────────┘
      │
      ▼
┌─────────────────────┐   TfidfVectorizer(max_features=5000)
│  Feature Extraction │   text → numeric feature matrix
└─────────────────────┘
      │
      ▼
┌─────────────────────┐   80 / 20 stratified split
│   Train/Test Split  │
└─────────────────────┘
      │
      ▼
┌───────────────────────────────────────────────────────────┐
│   Model Training & Evaluation                             │
│   Logistic Regression · Naive Bayes · Random Forest · MLP │
└───────────────────────────────────────────────────────────┘
      │
      ▼
   Best model selected by Accuracy / Precision / Recall / F1
```

## 🏗️ Tech Stack

| Category | Tools |
|---|---|
| Language | **Python 3** |
| Development environment | **Jupyter Notebook** |
| Data handling | **pandas**, **numpy** |
| NLP / text processing | **NLTK** (stopwords), `re`, `string` |
| Feature engineering | **scikit-learn** `TfidfVectorizer` |
| ML models | `LogisticRegression`, `MultinomialNB`, `RandomForestClassifier`, `MLPClassifier` (scikit-learn) |
| Evaluation | `accuracy_score`, `precision_score`, `recall_score`, `f1_score`, `confusion_matrix`, `classification_report` |
| Visualization | **matplotlib**, **seaborn** |
| Model persistence | **joblib** |
| Large file storage | **Git LFS** (dataset) |

## 📂 Repository Structure

```
Phishing-Email-Detection/
├── AI_Driven_Phishing_Email_Detection.ipynb    # Full pipeline: EDA → preprocessing → training → evaluation
├── Phishing Email Detection Report.pdf         # Written project report
├── phishing_email.csv                          # Dataset (tracked via Git LFS)
├── tfidf_vectorizer.pkl                        # Fitted TF-IDF vectorizer
├── logistic_regression.pkl                     # Trained Logistic Regression model
├── naive_bayes.pkl                             # Trained Multinomial Naive Bayes model
├── random_forest.pkl                           # Trained Random Forest model
└── neural_network.pkl                          # Trained MLP (Neural Network) model
```

## 📊 Dataset

- **82,486** email records, each labeled `0` (Legitimate) or `1` (Phishing)
- Near-balanced classes: **42,845 phishing** vs. **39,233 legitimate** emails
- After cleaning and deduplication: **82,078** samples used for feature extraction
- Split: **65,662** training samples / **16,416** testing samples (80/20 stratified)

> The dataset is tracked with **Git LFS**. Make sure Git LFS is installed before cloning, or the CSV will download as a small pointer file instead of the full data (see [Installation](#-installation--setup)).

## 📈 Results

All four models were trained on the same TF-IDF features and evaluated on the same held-out test set:

| Model | Accuracy | Precision | Recall | F1-Score |
|---|---|---|---|---|
| 🥇 **Neural Network (MLP)** | **98.28%** | 98.22% | 98.49% | 98.36% |
| Logistic Regression | 97.99% | 97.83% | 98.34% | 98.09% |
| Random Forest | 97.79% | 98.33% | 97.42% | 97.87% |
| Naive Bayes | 95.97% | 97.57% | 94.63% | 96.08% |

The **Neural Network** classifier achieved the highest overall accuracy and was selected as the best-performing model, closely followed by Logistic Regression and Random Forest.

## ⚙️ Installation & Setup

### Prerequisites

- Python 3.8+
- [Git LFS](https://git-lfs.com/) (required to pull the full dataset)
- Jupyter Notebook or JupyterLab

### Steps

```bash
# 1. Install Git LFS (one-time setup) and clone the repository
git lfs install
git clone https://github.com/kushjainv1903/Phishing-Email-Detection.git
cd Phishing-Email-Detection

# 2. Create and activate a virtual environment (recommended)
python -m .venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn nltk joblib notebook

# 4. Download NLTK stopwords (one-time setup)
python -c "import nltk; nltk.download('stopwords')"

# 5. Launch Jupyter and open the notebook
jupyter notebook AI_Driven_Phishing_Email_Detection.ipynb
```

## 🚀 Usage

### Option A — Run the full pipeline

Open `AI_Driven_Phishing_Email_Detection.ipynb` and run all cells top to bottom to reproduce data cleaning, TF-IDF vectorization, model training, evaluation, and visualization from scratch.

### Option B — Use the pre-trained models directly

Skip training entirely and classify new emails with the models already saved in this repo:

```python
import joblib
import re
import string
from nltk.corpus import stopwords

# Load the fitted vectorizer and the trained model of your choice
vectorizer = joblib.load("tfidf_vectorizer.pkl")
model = joblib.load("neural_network.pkl")   # or logistic_regression.pkl / random_forest.pkl / naive_bayes.pkl

stop_words = set(stopwords.words("english"))

def clean_text(text):
    text = text.lower()
    text = re.sub(r"http\S+|www\S+", "", text)
    text = re.sub(r"<.*?>", "", text)
    text = re.sub(r"\d+", "", text)
    text = text.translate(str.maketrans("", "", string.punctuation))
    words = [w for w in text.split() if w not in stop_words]
    return " ".join(words)

email_text = "Your account has been suspended. Click here to verify your details immediately."

cleaned = clean_text(email_text)
features = vectorizer.transform([cleaned])
prediction = model.predict(features)[0]

print("Phishing" if prediction == 1 else "Legitimate")
```

## 🗺️ Future Scope

- Integrate the trained model into an email client for real-time phishing detection
- Explore deep learning architectures such as LSTM and transformer-based models (BERT)
- Expand the dataset with more recent phishing email samples
- Build a web-based interface for live email classification
