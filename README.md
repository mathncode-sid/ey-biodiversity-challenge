# Biodiversity Challenge: Frog Species Classification

## Project Overview

This project implements machine learning models to predict the presence or absence of frog species across Australia using climate data from the **TerraClimate** dataset. The goal is to build a binary classification model achieving an **F1 Score of ~0.964** using climate variables as predictive features.

The challenge combines data from the **Global Biodiversity Information Facility (GBIF)** and **Microsoft Planetary Computer** to predict frog species distribution based on environmental conditions.

## Dataset

### Data Source
- **Training Data**: [Training_Data.csv](Training_Data.csv) - 5,000+ labeled samples
- **Test Data**: [Test.csv](Test.csv) - Unlabeled test set for predictions
- **Time Period**: 2017-2019
- **Geographic Coverage**: Australia

### Features
Each sample contains:
- **ID**: Unique identifier
- **Latitude / Longitude**: Geographic coordinates
- **Climate Variables** (8+ TerraClimate features):
  - Solar Radiation
  - Vapor Pressure
  - Temperature (min, max, mean)
  - Precipitation
  - Wind Speed
  - Soil Moisture
- **Occurrence Status**: Binary target variable (0 = absent, 1 = present)

## Project Structure

### Notebooks

#### 1. **Biodiversity_Challenge_Benchmark.ipynb**
The baseline model providing a solid foundation:
- Loads and explores GBIF and TerraClimate data
- Implements basic Logistic Regression classifier
- Establishes baseline F1 score and evaluation metrics
- Generates sample predictions

**Use this notebook** to understand the problem and get started quickly.

#### 2. **Frog_Model_Advanced.ipynb** ⭐ (Primary)
Advanced implementation with optimized models and techniques:
- Multiple classifier implementations:
  - Logistic Regression
  - Random Forest
  - Gradient Boosting (XGBoost/LightGBM)
  - Support Vector Machines (SVM)
- Comprehensive feature engineering and preprocessing
- Hyperparameter tuning and threshold optimization
- SMOTE for handling class imbalance
- Cross-validation and detailed evaluation metrics

**Use this notebook** for production-quality predictions and competitive results.

#### 3. **TerraClimate.ipynb**
Specialized notebook for climate data exploration:
- Retrieves and processes TerraClimate data from Microsoft Planetary Computer
- Data retrieval pipeline and quality checks
- Climate variable extraction and preprocessing
- Integration with GBIF occurrence data

## Key Methods & Techniques

### Machine Learning Models
- **Logistic Regression**: Fast baseline with interpretability
- **Random Forest**: Good balance between accuracy and interpretability
- **Gradient Boosting**: Often achieves best F1 scores
- **Support Vector Machines**: Robust non-linear classification

### Data Preprocessing
- ✅ Stratified train-validation splits (80/20)
- ✅ Feature scaling (StandardScaler/MinMaxScaler)
- ✅ Missing value imputation
- ✅ Class weight balancing for imbalanced data
- ✅ SMOTE (Synthetic Minority Over-sampling Technique)

### Model Optimization
- 🎯 **Hyperparameter Tuning**: Grid search and random search
- 🎯 **Threshold Tuning**: Optimizing decision boundary for F1 score
- 🎯 **Feature Engineering**: Creation of derived climate features
- 🎯 **Cross-Validation**: K-fold validation for robust evaluation

### Evaluation Metrics
- **F1 Score**: Primary metric (balance precision and recall)
- **Precision & Recall**: Class-specific performance
- **Confusion Matrix**: Error analysis
- **ROC-AUC**: Probability calibration
- **Classification Reports**: Detailed per-class metrics

## Results & Submissions

Multiple submission iterations tracking model improvements:

| Submission | Method | F1 Score (*) |
|-----------|--------|-------------|
| Baseline | Logistic Regression | ~0.47 |
| Hyperparameter Tuning | Gradient Boosting | 0.47+ |
| Feature Engineering | Random Forest + Features | 0.50+ |
| Threshold Tuning | Optimized GB | 0.57 |
| SMOTE | SMOTE + GB | 0.47 |

(*) Scores reflect F1 optimization on test threshold metrics

**Output Files**:
- [SampleSubmission.csv](SampleSubmission.csv) - Format template
- [Submission_*.csv](.) - Various model submissions

## Installation & Setup

### Prerequisites
- Python 3.8+
- Azure Storage access (for Planetary Computer data)
- Internet connection (for data downloads)

### Installation

1. **Clone/Download the project**
   ```bash
   cd ey-biodiversity-challenge
   ```

2. **Create and activate virtual environment**
   ```bash
   python -m venv .venv
   .\.venv\Scripts\Activate  # Windows
   source .venv/bin/activate  # macOS/Linux
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Quick Start (Baseline)
1. Open **Biodiversity_Challenge_Benchmark.ipynb**
2. Run all cells sequentially
3. Review baseline predictions and metrics

### Advanced Model (Recommended)
1. Open **Frog_Model_Advanced.ipynb**
2. Execute cells to:
   - Load and preprocess data
   - Train multiple classifiers
   - Perform hyperparameter tuning
   - Generate optimized predictions
3. Submit [Submission_*.csv](.) with predictions

### Climate Data Exploration
1. Open **TerraClimate.ipynb**
2. Retrieve climate variables from Planetary Computer
3. Visualize spatial and temporal patterns

## Dependencies

Key packages (see [requirements.txt](requirements.txt)):

```
pandas==3.0.2              # Data manipulation
scikit-learn==1.8.0        # ML models and preprocessing
xarray==2026.2.0           # N-dimensional arrays
pystac-client==0.9.0       # Planetary Computer SpatioTemporal Asset Catalog
planetary-computer==1.0.0  # Access climate data
matplotlib==3.10.8         # Visualization
seaborn==0.13.2           # Statistical visualization
tqdm==4.66.5              # Progress bars
fsspec==2026.3.0          # Cloud file systems
adlfs==2026.2.0           # Azure storage backend
```

## Workflow

```
1. Data Loading
   ├── GBIF frog occurrence data
   └── TerraClimate climate variables
   
2. Data Preprocessing
   ├── Missing value imputation
   ├── Feature scaling
   └── Class imbalance handling (SMOTE)
   
3. Feature Engineering
   ├── Climate feature extraction
   ├── Derived feature creation
   └── Feature selection
   
4. Model Training
   ├── Train-validation split
   ├── Hyperparameter tuning
   └── Cross-validation
   
5. Evaluation & Optimization
   ├── F1 score calculation
   ├── Threshold tuning
   └── Metric analysis
   
6. Prediction & Submission
   ├── Test set prediction
   ├── Format validation
   └── Submit [Submission_*.csv]
```

## Key Insights

### What Works Well
- ✅ Gradient Boosting models achieve the best F1 scores
- ✅ Climate variables are strong predictors (especially temperature and precipitation)
- ✅ SMOTE helps with class imbalance but requires threshold optimization
- ✅ Feature engineering improves model robustness

### Class Imbalance Challenge
- Dataset has significant class imbalance (more absence than presence records)
- Solutions: class weighting, SMOTE, threshold optimization
- F1 score is critical to balance precision and recall

### Geographic Patterns
- Frog presence correlates with specific temperature and moisture ranges
- Regional climate variations create distinct habitat zones
- Ensemble methods capture geographic patterns better than single models

## Notes for Improvement

1. **Feature Engineering**: Explore interaction terms and polynomial features
2. **Ensemble Methods**: Stack multiple models for better predictions
3. **Hyperparameter Optimization**: Use Bayesian optimization (Optuna)
4. **Data Augmentation**: Generate synthetic geographic patterns
5. **Model Interpretability**: Use SHAP values to understand feature importance

## File Structure

```
ey-biodiversity-challenge/
├── Biodiversity_Challenge_Benchmark.ipynb    # Baseline model
├── Frog_Model_Advanced.ipynb                 # Advanced model ⭐
├── TerraClimate.ipynb                        # Climate data pipeline
├── Training_Data.csv                         # Training set
├── Test.csv                                  # Test set
├── SampleSubmission.csv                      # Submission format
├── Submission_*.csv                          # Model submissions
├── requirements.txt                          # Python dependencies
├── README.md                                 # This file
└── README_Advanced_Guide.md                  # Detailed technical guide
```

## References

- **GBIF (Global Biodiversity Information Facility)**: https://www.gbif.org/
- **Microsoft Planetary Computer**: https://planetarycomputer.microsoft.com/
- **TerraClimate Dataset**: https://www.climatologylab.org/terraclimate.html
- **scikit-learn Documentation**: https://scikit-learn.org/

## Next Steps

1. Start with **Biodiversity_Challenge_Benchmark.ipynb** for understanding
2. Move to **Frog_Model_Advanced.ipynb** for optimized predictions
3. Experiment with different hyperparameters and feature combinations
4. Submit best predictions to the challenge

## Author Notes

This project demonstrates:
- Data acquisition from cloud-based climate services
- End-to-end machine learning pipeline
- Handling of imbalanced classification problems
- Model optimization for specific metrics (F1 Score)
- Geographic/environmental data analysis

---

**Challenge**: EY Biodiversity Challenge  
**Target F1 Score**: ~0.964  
**Dataset Size**: 5,000+ samples  
**Model**: Gradient Boosting with climate features

Good luck with the challenge! 🐸🌍
