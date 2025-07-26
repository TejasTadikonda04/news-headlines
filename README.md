# News Headlines Sentiment Analysis

A comprehensive sentiment analysis project that compares two different approaches for analyzing the sentiment polarity of news headlines over time: a custom-trained SVM model and a pre-trained TextBlob model.

## 📖 Overview

This project analyzes the sentiment polarity of news headlines from ABC News (2003-2021) using two distinct methodologies:

1. **Original Model**: A custom Support Vector Machine (SVM) classifier trained on the Sentiment140 dataset
2. **Pre-trained Model**: TextBlob's built-in sentiment analysis capabilities

The goal is to track how news sentiment has evolved over nearly two decades and compare the effectiveness of different sentiment analysis approaches.

## 📁 Project Structure

```
news-headlines/
├── original-model/
│   └── original-model.ipynb     # Custom SVM sentiment analysis
├── pre-trained/
│   └── pre-trained-model.ipynb  # TextBlob-based sentiment analysis
├── .gitignore                   # Excludes CSV and pickle files
└── README.md                    # This file
```

## 🎯 Features

### Original Model (SVM-based)
- **Custom Training**: Trains an SVM classifier on the Sentiment140 dataset (1.6M tweets)
- **Text Preprocessing**: NLTK-based text cleaning with stopword removal and tokenization
- **TF-IDF Vectorization**: Converts text to numerical features using TF-IDF (5000 max features)
- **Model Persistence**: Saves trained model and vectorizer for reuse
- **Performance**: Achieves 77% accuracy on test data
- **Sentiment Scale**: Uses -1 (negative), 0 (neutral), 1 (positive)

### Pre-trained Model (TextBlob)
- **Ready-to-use**: Leverages TextBlob's pre-trained sentiment analyzer
- **Polarity Score**: Returns continuous values between -1 and 1
- **No Training Required**: Immediate analysis without model training
- **Lightweight**: Minimal computational requirements

### Analysis Features
- **Temporal Analysis**: Groups sentiment by year (2003-2021)
- **Data Visualization**: Matplotlib plots showing sentiment trends over time
- **CSV Export**: Exports results for further analysis
- **Comparative Study**: Enables comparison between custom and pre-trained approaches

## 📊 Datasets

### Primary Dataset
- **ABC News Headlines**: `abcnews-date-text.csv`
  - Source: ABC News Australia
  - Time Range: 2003-2021
  - Content: Date-stamped news headlines
  - Format: CSV with date and headline text columns

### Training Dataset (Original Model Only)
- **Sentiment140**: `training.1600000.processed.noemoticon.csv`
  - Source: Stanford Sentiment140 dataset
  - Size: 1.6 million tweets
  - Labels: Binary sentiment (0=negative, 4=positive)
  - Usage: 10% sample used for training due to computational constraints

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas scikit-learn nltk textblob matplotlib joblib
```

### Required Data Files

You'll need to download these datasets:

1. **ABC News Headlines Dataset**
   - File: `abcnews-date-text.csv`
   - Place in project root directory

2. **Sentiment140 Dataset** (for original model)
   - File: `training.1600000.processed.noemoticon.csv`
   - Place in project root directory
   - Available from: Stanford Sentiment140 project

### Usage

#### Running the Pre-trained Model
```bash
jupyter notebook pre-trained/pre-trained-model.ipynb
```

#### Running the Original Model
```bash
jupyter notebook original-model/original-model.ipynb
```

## 📈 Results and Performance

### Original Model Performance
- **Accuracy**: 77%
- **Precision**: 0.77 (macro avg)
- **Recall**: 0.77 (macro avg)
- **F1-Score**: 0.77 (macro avg)

### Output Files Generated
- `pre_trained_polarity.csv`: TextBlob sentiment results by date
- `pre_trained_polarity_by_year.csv`: TextBlob results grouped by year
- `original_polarity.csv`: SVM model sentiment results by date
- `original_polarity_by_year.csv`: SVM results grouped by year
- `svm_model.pkl`: Trained SVM model
- `tfidf_vectorizer.pkl`: Fitted TF-IDF vectorizer

## 🔧 Technical Implementation

### Original Model Workflow
1. **Data Loading**: Load and preprocess Sentiment140 dataset
2. **Sampling**: Use 10% of data (160K tweets) for computational efficiency
3. **Text Preprocessing**: Remove stopwords, tokenize, clean text
4. **Feature Extraction**: TF-IDF vectorization with 5000 features
5. **Model Training**: Train linear SVM classifier
6. **Model Evaluation**: Test on held-out data
7. **Application**: Apply to ABC News headlines
8. **Analysis**: Group by year and visualize trends

### Pre-trained Model Workflow
1. **Data Loading**: Load ABC News headlines
2. **Sentiment Analysis**: Apply TextBlob sentiment analysis
3. **Data Processing**: Group results by year
4. **Visualization**: Plot sentiment trends over time

## 📊 Data Processing

### Text Preprocessing (Original Model)
- Tokenization using NLTK
- Stopword removal (English)
- TF-IDF vectorization
- Maximum 5000 features

### Sentiment Mapping
- **Original Model**: Discrete values (-1, 0, 1)
- **Pre-trained Model**: Continuous values (-1.0 to 1.0)

## 🔍 Analysis Insights

The project enables comparison of:
- **Custom vs. Pre-trained**: Performance differences between approaches
- **Temporal Trends**: How news sentiment evolved from 2003-2021
- **Model Characteristics**: Speed vs. accuracy trade-offs
- **Implementation Complexity**: Training requirements vs. ease of use

## 🛠️ Dependencies

### Core Libraries
- `pandas`: Data manipulation and analysis
- `scikit-learn`: Machine learning algorithms and metrics
- `nltk`: Natural language processing
- `textblob`: Pre-trained sentiment analysis
- `matplotlib`: Data visualization
- `joblib`: Model serialization

### NLTK Data Requirements
```python
nltk.download('stopwords')
nltk.download('punkt')
```

## 📝 Notes

- The original model uses only 10% of the Sentiment140 dataset for training
- CSV and pickle files are gitignored to avoid repository bloat
- Both models analyze the same ABC News dataset for comparison
- Results are exported as CSV files for further analysis
- Visualizations show sentiment trends over the 2003-2021 period

## 🤝 Contributing

Feel free to fork this project and submit pull requests for improvements such as:
- Additional sentiment analysis models
- Enhanced text preprocessing
- More sophisticated visualization
- Extended time range analysis
- Model performance improvements

## 📄 License

This project is open source and available under the MIT License.
