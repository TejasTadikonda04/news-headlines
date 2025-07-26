# News-Headlines Sentiment Analysis

A Python project that explores how the sentiment of Australian Broadcasting Corporation (ABC) news headlines has evolved from 2003 – 2021.  
Two independent pipelines are provided:

1. **Pre-trained approach** – a lightweight baseline that uses the sentiment analyser built into `TextBlob`.
2. **Original model approach** – a custom Support Vector Machine (SVM) classifier trained from scratch on the 1.6 M tweet **Sentiment140** corpus.

Both pipelines predict the polarity of every headline, aggregate the scores by year and produce an interactive time-series visualisation.

---

## Table of Contents
1. [Project Motivation](#project-motivation)
2. [Data Sources](#data-sources)
3. [Repository Structure](#repository-structure)
4. [Quick-start](#quick-start)
   * [Prerequisites](#prerequisites)
   * [Installation](#installation)
   * [Dataset download](#dataset-download)
   * [Running the notebooks](#running-the-notebooks)
5. [Understanding the Output](#understanding-the-output)
6. [Extending this Work](#extending-this-work)
7. [Troubleshooting](#troubleshooting)
8. [License](#license)
9. [Citation](#citation)

---

## Project Motivation
News headlines are designed to be punchy and emotionally engaging.  Measuring their sentiment over time can reveal how news media frames events, crises and public mood.  

This project asks:
> *"Has the average sentiment of ABC online headlines become more negative, positive or remained neutral over the last two decades?"*

To answer this we
1. Parse **1.1 M** news headlines released by the ABC from 2003-2021.
2. Apply two sentiment-analysis strategies (pre-trained vs custom) to each headline.
3. Compare yearly average polarity scores.
4. Visualise the trend.

---

## Data Sources
| Dataset | Description | Size | License |
|---------|-------------|------|---------|
| **ABC News Headlines** | `abcnews-date-text.csv` contains 1 ,101 ,146 headlines from 2003-2021 with publication dates.  | ~225 MB | [CC BY 3.0 AU](https://creativecommons.org/licenses/by/3.0/au/) |
| **Sentiment140** | `training.1600000.processed.noemoticon.csv` – 1.6 M labelled tweets used to train the custom SVM. | ~245 MB | [GPL-2.0](https://github.com/karthikncode/sentiment140/blob/master/LICENSE) |

> ⚠️ Both CSVs are **ignored** by Git via `.gitignore` → download them manually (see below).

---

## Repository Structure
```text
.
├── original-model/            # notebook that builds & applies custom SVM
│   └── original-model.ipynb
├── pre-trained/               # notebook that uses TextBlob
│   └── pre-trained-model.ipynb
├── .gitignore                 # ignores large data & model artefacts
├── README.md                  # ← you are here
└── requirements.txt           # python dependencies (generated on first run)
```
Additional artefacts created when you execute the notebooks (CSV exports, `.pkl` models, figures) live next to the notebooks and are excluded from version control.

---

## Quick-start
### Prerequisites
* Python **3.9** or newer
* Git
* (Recommended) **virtualenv** / **conda**

### Installation
```bash
# 1. Clone the repository
$ git clone https://github.com/<your-username>/news-headlines.git
$ cd news-headlines

# 2. Create & activate a virtual environment
$ python -m venv .venv
$ source .venv/bin/activate  # Windows: .venv\Scripts\activate

# 3. Install dependencies
#    A requirements.txt will be generated automatically by the cell that imports packages, 
#    but you can pre-create one as follows:
$ pip install -r requirements.txt  # OR run notebooks and let them install on-demand
```

> If `requirements.txt` is missing, simply install the packages listed inside each notebook header:
> `pandas`, `numpy`, `scikit-learn`, `nltk`, `textblob`, `matplotlib`, `joblib`, `jupyter`.

### Dataset download
1. **ABC News Headlines** – download from [Kaggle](https://www.kaggle.com/competitions/into-the-unknown-k3k11/data) (direct file: `abcnews-date-text.csv`).
2. **Sentiment140** – download from [Kaggle](https://www.kaggle.com/datasets/kazanova/sentiment140) (file: `training.1600000.processed.noemoticon.csv`).

Place both CSVs in the project **root** so the relative paths used inside the notebooks resolve correctly.

### Running the notebooks
```bash
$ jupyter lab  # or 'jupyter notebook'
```
Open:
* `pre-trained/pre-trained-model.ipynb` – fastest way to reproduce the analysis (≈ 5 min on commodity hardware).
* `original-model/original-model.ipynb` – trains the SVM (≈ 30 – 40 min, memory intensive) then performs the same analysis.

Each notebook is **self-contained** and can be executed top-to-bottom.  Intermediate artefacts (vectoriser & model `.pkl`s, yearly polarity CSVs) are written to disk for reuse.

---

## Understanding the Output
After successful execution you will obtain:

* `pre_trained_polarity.csv` / `original_polarity.csv` – polarity for **every** headline.
* `pre_trained_polarity_by_year.csv` / `original_polarity_by_year.csv` – polarity lists grouped by year.
* A line plot named *“Polarity of newspaper headlines over time”* embedded in the notebook.

Interpretation tips:
* **+1.0** → extremely positive, **0** → neutral, **-1.0** → extremely negative.
* Compare the shape of the curves from the two methods. Large divergences may indicate limitations of TextBlob or the custom model.

---

## Extending this Work
* **Model upgrade** – swap the SVM for a transformer-based classifier (e.g. `DistilBERT` fine-tuned on Sentiment140).
* **Granularity** – segment by month or topic instead of year.
* **Geographic comparison** – apply the pipeline to other news outlets.
* **Deployment** – wrap the models into a REST API or Streamlit dashboard.

Feel free to open an issue or pull request if you build something interesting!

---

## Troubleshooting
| Problem | Possible fix |
|---------|--------------|
| `LookupError: Resource stopwords not found` | Run the `nltk.download('stopwords')` cell inside the notebook (already included). |
| Notebook crashes during SVM fitting | Use a machine with ≥ 8 GB RAM or reduce `frac` in the training sample step (defaults to 10 %). |
| Empty plot / NaNs in average polarity | Verify that the CSV paths are correct and that the datasets were downloaded in full. |

---

## License
This repository is released under the **MIT License**.  
Separate datasets retain their original licenses (see links above).

---

## Citation
If you use this code in academic work please cite as:

> *Author*. (2023). **News-Headlines Sentiment Analysis** [Computer software]. GitHub. https://github.com/your-username/news-headlines

---

*Happy analysing!*
