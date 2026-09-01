# 🧠 AI-Generated vs Human-Written Text Detection

A machine-learning and NLP project for classifying text as **AI-generated** or **human-written**, combining text preprocessing, hybrid feature engineering, traditional machine learning, RoBERTa-based deep learning, ensemble learning, and a Streamlit interface.

> **Important:** AI-text detection is probabilistic. The system should be treated as an analytical aid rather than definitive proof of authorship.

---

## 📌 Project Overview

With the rapid growth of Large Language Models (LLMs), distinguishing AI-generated content from human-written text has become an important NLP problem across education, research, publishing, and content verification.

This project implements an end-to-end AI text detection pipeline combining:

- Natural Language Processing (NLP)
- Machine Learning (ML)
- Deep Learning with RoBERTa
- Hybrid feature engineering
- Semantic embeddings
- Ensemble learning
- Streamlit deployment
- Real-time text classification

### Classification Labels

| Label | Meaning |
|---|---|
| `0` | Human Written |
| `1` | AI Generated |

---

## 🎯 Key Features

- Complete NLP preprocessing pipeline
- Text cleaning and normalization
- Duplicate and empty-record handling
- Train/test data splitting
- Class balancing
- TF-IDF feature extraction
- Stylometric features
- POS-based linguistic features
- Semantic embeddings using `all-MiniLM-L6-v2`
- Logistic Regression
- XGBoost
- Stacking / ensemble learning
- RoBERTa transformer model
- Weighted ensemble prediction
- Accuracy, Precision, Recall and F1 evaluation
- Streamlit web interface
- Confidence/probability output
- Real-time inference

---

## 🏗️ System Architecture

```text
Raw Dataset
     │
     ▼
Text Preprocessing
     │
     ├── Lowercasing
     ├── URL Removal
     ├── Special Character Removal
     ├── Number Removal
     ├── Tokenization
     ├── Stopword Removal
     └── Lemmatization
     │
     ▼
Dataset Cleaning & Splitting
     │
     ├── Duplicate Removal
     ├── Empty Text Removal
     ├── Class Balancing
     └── Train/Test Split
     │
     ▼
Hybrid Feature Engineering
     │
     ├── TF-IDF
     ├── Stylometric Features
     ├── POS Features
     └── Semantic Embeddings
     │
     ├───────────────────────┐
     ▼                       ▼
Traditional ML          RoBERTa Transformer
     │                       │
     ├── Logistic Regression │
     └── XGBoost             │
     │                       │
     └──────────┬────────────┘
                ▼
        Ensemble Prediction
                │
                ▼
           Evaluation
                │
                ▼
      Streamlit Deployment
                │
                ▼
       AI / Human Prediction
```

---

## 📚 Research Foundation

This project is based on research related to AI-generated text detection.

### Research Paper

Research material:

https://drive.google.com/drive/folders/1dELjl1SUJa16CEklBh8yKLnPaFNmKM2i?usp=drive_link

### Dataset Source

**CHEAT Dataset — IEEE Abstract Dataset**

https://github.com/botianzhe/CHEAT

### Dataset Usage Notice

The dataset is obtained from the original research source and is **not included in this repository** because of dataset licensing, copyright considerations, and repository-size limitations.

Please obtain the dataset directly from its original source and follow its applicable license and usage requirements.

---

## 📊 Dataset Information

The project uses the following source files:

| File | Label |
|---|---|
| `ieee-init.xlsx` | Human |
| `ieee-chatgpt-generation.xlsx` | AI |
| `ieee-chatgpt-polish.xlsx` | AI |
| `ieee-chatgpt-fusion.xlsx` | AI |

### Dataset Statistics

The project documentation reports approximately:

- **Total samples:** ~50,000
- **Human samples:** ~15,000
- **AI samples:** ~35,000

Dataset availability and exact counts may depend on the version of the source data used during experimentation.

---

## 🧹 Text Preprocessing

Main preprocessing implementation:

```text
preprocessing/preprocess.py
```

### Operations

- Lowercasing
- URL removal
- Special-character removal
- Number removal
- Tokenization
- Stopword removal
- Lemmatization

### Output

```text
data/final_preprocessed_data.csv
```

Expected columns:

```text
clean_text
label
```

---

## 🔀 Dataset Splitting

Main implementation:

```text
models/data_split.py
```

### Processing

- Removes duplicate records
- Removes empty text samples
- Balances class distribution
- Helps prevent data leakage
- Creates training and testing sets

### Split

| Dataset | Percentage |
|---|---:|
| Training | 80% |
| Testing | 20% |

Generated files:

```text
train_data.csv
test_data.csv
```

---

## 🧠 Hybrid Feature Engineering

Implementation:

```text
features/hybrid_features_from_split.py
```

The project combines several types of text representations.

### 1. TF-IDF Features

- Unigrams
- Bigrams
- Maximum features: `5000`

### 2. Stylometric Features

Examples include:

- Average word length
- Average sentence length
- Stopword ratio
- Readability metrics

### 3. POS-Based Features

Examples include:

- Noun ratio
- Verb ratio
- Adjective ratio
- Adverb ratio

### 4. Semantic Features

Embedding model:

```text
all-MiniLM-L6-v2
```

Embedding dimension:

```text
384
```

### Combined Feature Vector

The project documentation reports:

```text
5,395 features per sample
```

---

## 🤖 Traditional Machine Learning

Implementation:

```text
models/train_models.py
```

### Models

1. Logistic Regression
2. XGBoost
3. Stacking Ensemble

The project documentation reports Logistic Regression as the strongest traditional ML model, with approximately **86% accuracy** in the reported experiment.

> Reported results are experiment-specific and should not be interpreted as universal model performance.

---

## 🧠 RoBERTa Deep Learning Model

Implementation:

```text
models/train_roberta.py
```

Transformer:

```text
roberta-base
```

### Training Configuration

| Parameter | Value |
|---|---|
| Model | `roberta-base` |
| Epochs | 3 |
| Maximum sequence length | 256 |
| GPU | Enabled during training |

---

## 🔥 Ensemble Learning

The documented final prediction combines the transformer and traditional ML predictions:

```text
Final Prediction =
0.7 × RoBERTa
+
0.3 × Logistic Regression
```

### Why Ensemble?

**RoBERTa** contributes:

- Context understanding
- Semantic representation
- Deep language understanding

**Logistic Regression** contributes:

- Statistical writing patterns
- Vocabulary distribution
- Feature-based classification

Combining the two approaches is intended to leverage complementary signals.

---

## 📊 Performance Evaluation

Evaluation implementation:

```text
evaluation/evaluate.py
```

### Metrics

The project evaluates models using:

- Accuracy
- Precision
- Recall
- F1 Score

### Reported Accuracy

| Model | Reported Accuracy |
|---|---:|
| Logistic Regression | ~86% |
| RoBERTa | ~89% |
| Ensemble Model | ~90% |

### Performance Note

The current documentation supports an approximate **89–90% accuracy** result for the final system.

The README intentionally does **not** state a specific F1-score result because a verified measured F1 value is not currently documented here.

If a reproducible evaluation run produces an exact F1 score, it can be added to this section with the corresponding evaluation output.

---

## 🚀 Streamlit Application

Application entry point:

```text
app.py
```

The Streamlit application provides a web interface for text classification.

### Application Features

- Text input
- AI/Human classification
- Confidence/probability scores
- Prediction output
- Real-time inference

### Run the Application

```bash
streamlit run app.py
```

---

## 🌐 Live Demo

The project is currently deployed at:

https://chiragpawar.vercel.app/

---

## 📸 Application Screenshots

### 1. Application Interface

![AI vs Human Text Detector](screenshots/application-interface.png)

### 2. Prediction Result

![Prediction Result](screenshots/prediction-result.png)

> Make sure the two image files exist in the `screenshots/` directory with exactly these filenames.

---

## 📦 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/LeutnantMutig/AI-vs-Human-Text-Detection.git
cd AI-vs-Human-Text-Detection
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

### 3. Activate the Environment

#### Windows

```powershell
venv\Scripts\activate
```

#### Linux / macOS

```bash
source venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Run the Application

```bash
streamlit run app.py
```

---

## 🏋️ Training From Scratch

If you want to reproduce the documented training pipeline, run the stages in order.

### Step 1 — Preprocessing

```bash
python preprocessing/preprocess.py
```

### Step 2 — Dataset Split

```bash
python models/data_split.py
```

### Step 3 — Hybrid Feature Engineering

```bash
python features/hybrid_features_from_split.py
```

### Step 4 — Train Traditional Models

```bash
python models/train_models.py
```

### Step 5 — Train RoBERTa

```bash
python models/train_roberta.py
```

> Training the transformer model may require substantial compute resources and can take significantly longer than the preprocessing and traditional ML stages.

---

## 📥 Pretrained Models

Pretrained RoBERTa model files are not stored directly in this repository because of repository-size limitations.

Download the available pretrained model files from:

https://drive.google.com/drive/folders/1ORZli3qaT7Oo8f3AN9XfE-dJ82crCiNN?usp=drive_link

Place the downloaded files in:

```text
models/saved/
```

---

## 📁 Project Structure

```text
AI-vs-Human-Text-Detection/
│
├── data/
├── preprocessing/
├── features/
├── models/
├── evaluation/
├── screenshots/
│   ├── application-interface.png
│   └── prediction-result.png
│
├── app.py
├── requirements.txt
├── README.md
├── LICENSE
└── .gitignore
```

The exact working-tree contents can vary depending on local/generated files that are intentionally excluded by `.gitignore`.

---

## ⚠️ Limitations

AI-generated text detection has important limitations.

- Human and AI writing styles can overlap.
- Academic or highly formal writing may be misclassified.
- Model performance depends on dataset quality and diversity.
- Newer or unseen language models may behave differently from the training data.
- Detection confidence is not proof of authorship.
- Results may change when the dataset, preprocessing pipeline, threshold, or model configuration changes.
- Generalization to real-world text outside the training distribution requires additional validation.

---

## 🔬 Reproducibility Notes

For meaningful reproduction of the reported results:

1. Use the intended source dataset.
2. Follow the preprocessing pipeline.
3. Use the documented train/test split procedure.
4. Keep model and feature configurations consistent.
5. Run the evaluation script on the resulting models.
6. Record the exact dataset version, random seeds, and evaluation outputs.

When reporting new results, include the actual measured metrics rather than estimated or rounded values.

---

## 🛠️ Technology Stack

| Category | Technology |
|---|---|
| Language | Python |
| NLP | NLTK / text preprocessing |
| Feature Engineering | TF-IDF, stylometric and POS features |
| Semantic Embeddings | Sentence Transformers / `all-MiniLM-L6-v2` |
| Traditional ML | Scikit-learn |
| Gradient Boosting | XGBoost |
| Deep Learning | PyTorch / Transformers |
| Transformer | RoBERTa |
| Web Interface | Streamlit |
| Version Control | Git / GitHub |

---

## 📌 Project Workflow Summary

```text
Dataset
   ↓
Preprocessing
   ↓
Cleaning & Deduplication
   ↓
Train/Test Split
   ↓
Hybrid Feature Engineering
   ↓
Traditional ML ──────┐
                     ├──► Ensemble ───► Evaluation
RoBERTa ─────────────┘
                                      ↓
                                Streamlit App
                                      ↓
                              AI / Human Result
```

---

## 🏁 Conclusion

This project demonstrates an end-to-end NLP workflow for AI-generated versus human-written text classification.

It combines:

- Text preprocessing
- Feature engineering
- Traditional machine learning
- Semantic embeddings
- Transformer-based deep learning
- Ensemble learning
- Model evaluation
- Streamlit deployment

The documented experiments report approximately **90% accuracy** for the final ensemble approach.

The project is intended as an applied NLP and machine-learning demonstration and should be further validated before being used for high-stakes authorship decisions.

---

## 👨‍💻 Author

**Chirag Pawar**

B.Tech Computer Science Engineering (AI & ML)

- GitHub: https://github.com/LeutnantMutig
- LinkedIn: https://www.linkedin.com/in/chiragpawar01

---

## ⭐ Support

If you find this project useful:

- ⭐ Star the repository
- 🍴 Fork the project
- 📢 Share it with others
- 💬 Provide feedback or suggestions

---

## 📄 License

This project is licensed under the **MIT License**. See the [`LICENSE`](LICENSE) file for details.
