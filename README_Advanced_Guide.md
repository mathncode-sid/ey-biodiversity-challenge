# Advanced Frog Prediction Model - Complete Guide

## Overview
This project builds a machine learning classification model to predict frog species presence based on TerraClimate climate variables. The model aims to achieve an F1 Score close to the leaderboard top (0.964).

## Project Structure
- **Training_Data.csv**: Training dataset with frog presence/absence labels
- **Test.csv**: Test dataset (without labels) for final predictions
- **TerraClimate.ipynb**: Notebook to extract climate variables and generate GeoTIFF files
- **Frog_Model_Advanced.ipynb**: Main model building notebook (improved from benchmark)
- **Biodiversity_Challenge_Benchmark.ipynb**: Baseline benchmark model

## Key Improvements Over Benchmark

The advanced model includes:

1. **Multiple Climate Variables**: Uses 8+ TerraClimate variables instead of just 2
   - Solar radiation (srad)
   - Vapor pressure (vap)
   - Temperature metrics (tmin, tmax, tmean)
   - Precipitation (pr)
   - Wind speed (ws)
   - Soil moisture

2. **Multiple Algorithms**:
   - Logistic Regression (baseline)
   - Random Forest (good accuracy)
   - Gradient Boosting (often best for F1)
   - SVM (robust classification)

3. **Better Preprocessing**:
   - Stratified train-validation split (maintains class balance)
   - Feature scaling appropriate to each model
   - Handling of missing values
   - Class weight balancing to handle imbalanced data

4. **Performance Evaluation**:
   - F1 Score focused (as per challenge requirement)
   - Classification reports and confusion matrices
   - Feature importance analysis

## Step-by-Step Usage

### Step 1: Prepare Climate Data
First, you need to generate the TerraClimate GeoTIFF file:
```
1. Open TerraClimate.ipynb
2. Run all cells to download and process climate data
3. This generates: TerraClimate_output.tiff
```

### Step 2: Run Advanced Model
```
1. Open Frog_Model_Advanced.ipynb
2. Run cells sequentially
3. The notebook will:
   - Load training and test data
   - Extract climate features from GeoTIFF
   - Train 4 different models
   - Select the best one based on F1 Score
   - Generate predictions on test set
   - Create submission file
```

### Step 3: Submit Predictions
```
1. Find the generated submission file: Submission_*.csv
2. Check it has the correct format:
   - 2 columns: ID and Target
   - Target values are 0 or 1
3. Submit to the challenge platform
```

## Hyperparameter Tuning for Better Performance

To improve F1 Score beyond 0.96:

### Random Forest Tuning:
```python
params = {
    'n_estimators': [100, 200, 300],
    'max_depth': [10, 15, 20],
    'min_samples_split': [2, 5, 10],
    'min_samples_leaf': [1, 2, 4],
}
```

### Gradient Boosting Tuning:
```python
params = {
    'n_estimators': [100, 200, 300],
    'learning_rate': [0.01, 0.05, 0.1],
    'max_depth': [3, 5, 7],
    'subsample': [0.7, 0.8, 0.9],
}
```

### SVM Tuning:
```python
params = {
    'C': [0.1, 1, 10, 100],
    'gamma': ['scale', 'auto'],
    'kernel': ['rbf', 'poly'],
}
```

## Advanced Feature Engineering Ideas

1. **Temporal Features**: Create time-based aggregations
   - Monthly averages
   - Seasonal patterns
   - Anomalies from normal conditions

2. **Interaction Features**: Combine variables
   - Temperature × Humidity
   - Precipitation × Soil Moisture
   - Temperature range (tmax - tmin)

3. **Statistical Features**: Aggregate over time windows
   - Rolling means
   - Standard deviations
   - Min/max over periods

4. **Domain Features**: Climate indices
   - NDVI (vegetation index)
   - Humidity index
   - Drought index

## Models Comparison

| Model | Pros | Cons |
|-------|------|------|
| Logistic Regression | Fast, interpretable, baseline | Limited to linear patterns |
| Random Forest | Good accuracy, feature importance, robust | Prone to overfitting, slower |
| Gradient Boosting | Often best F1 Score, powerful | Complex, requires tuning |
| SVM | Works well, good generalizer | Slow for large datasets |

## Common Issues and Solutions

### Issue: Low F1 Score
- **Solution**: Use more TerraClimate variables (generate full GeoTIFF)
- **Solution**: Tune hyperparameters with GridSearchCV
- **Solution**: Create domain-specific features

### Issue: Model Overfitting
- **Solution**: Reduce model complexity (smaller trees, less features)
- **Solution**: Increase validation set size
- **Solution**: Add regularization (L1/L2)

### Issue: Class Imbalance
- **Solution**: Use class_weight='balanced' in models
- **Solution**: Use SMOTE or other resampling
- **Solution**: Adjust classification threshold

## Submission Format

The submission file should be CSV with exactly 2 columns:

```
ID,Target
ID_TS_54240C,0
ID_TS_EF9635,1
ID_TS_4E63E6,0
...
```

## Performance Tracking

Keep track of your results:
```
Model                  | F1 Score | Features Used
Benchmark (2 features) | ~0.85    | srad, vap
Advanced RF (8 vars)   | ~0.92    | all TerraClimate
Tuned GB               | ~0.94    | all TerraClimate + tuned
Ensemble               | ~0.96    | voting classifier
```

## Next Optimization Strategies

1. **Ensemble Methods**:
   - Voting Classifier
   - Stacking
   - Blending multiple models

2. **Cross-Validation**:
   - 5-fold stratified CV
   - Nested CV for hyperparameter tuning

3. **Feature Selection**:
   - RFE (Recursive Feature Elimination)
   - Correlation analysis
   - Feature importance thresholding

4. **Threshold Optimization**:
   - Find optimal classification threshold
   - Maximize F1 Score specifically

5. **Data Augmentation**:
   - Oversample minority class
   - Undersampling majority class
   - SMOTE

## Resources

- [TerraClimate Documentation](https://www.climatologylab.org/terraclimate.html)
- [Scikit-learn Documentation](https://scikit-learn.org/)
- [F1 Score Explanation](https://en.wikipedia.org/wiki/F-score)
- [FrogID Project](https://frogid.nswildlife.org.au/)

## Final Tips for Success

✓ Always validate on a held-out set first before submitting  
✓ Focus on F1 Score, not accuracy (use stratified split)  
✓ Explore multiple algorithms - they often give different insights  
✓ Use feature importance to understand model decisions  
✓ Document your experiments for reproducibility  
✓ Don't use lat/lon as features - use climate data only  
✓ Consider ensemble methods for best performance  
