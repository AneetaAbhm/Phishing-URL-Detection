

#  **PHISHING URL DETECTION**

---

## 1. **Overview of Problem Statement**
Phishing attacks are one of the most common cyber threats, costing individuals and organizations billions annually. Attackers use deceptive URLs to steal sensitive information like passwords, credit card details, and personal data.  
Traditional methods like blacklists fail to catch newly emerging phishing URLs. Therefore, this project leverages **machine learning** to create a proactive phishing detection system by analyzing URL features and classifying them as either **phishing** or **legitimate**.

---

## 2. **Objective**
Develop a robust machine learning model to classify URLs as either **phishing** or **legitimate** based on their characteristics and metadata.  
The system is designed for **real-time classification**, offering protection against evolving phishing techniques by detecting suspicious patterns and behaviors.

---

## 3. **Data Description**
The dataset consists of **URL-based, content-based, and website behavior-based** features to identify phishing patterns. Below is a detailed explanation of the key features:

### **URL & Domain-Based Features**
- **URL**: The full web address being analyzed.  
- **URLLength**: Length of the URL string.  
- **Domain**: The main domain of the URL (e.g., `example.com`).  
- **DomainLength**: Length of the domain name.  
- **IsDomainIP**: Indicates if the domain is an IP address (1 = Yes, 0 = No).  
- **TLD**: Top-level domain (e.g., `.com`, `.org`).  
- **TLDLegitimateProb**: Probability that the TLD is legitimate.  
- **NoOfSubDomain**: Number of subdomains.  
- **IsHTTPS**: Indicates whether the URL uses HTTPS (1 = Yes, 0 = No).  

### **Character-Based Features**
- **NoOfLettersInURL**: Number of alphabetic characters in the URL.  
- **NoOfDigitsInURL**: Number of numeric digits.  
- **DigitRatioInURL**: Ratio of digits to total URL length.  
- **SpecialCharRatioInURL**: Ratio of special characters in the URL.  
- **NoOfEqualsInURL**: Number of `=` characters.  
- **NoOfQMarkInURL**: Number of `?` characters.  
- **NoOfAmpersandInURL**: Number of `&` characters.  

### **Web Page Content & Behavior Features**
- **HasTitle**: Whether the webpage has a `<title>` tag.  
- **TitleLength**: Length of the `<title>` tag content.  
- **HasFavicon**: Whether the page has a favicon.  
- **NoOfPopup**: Number of pop-ups on the webpage.  
- **NoOfiFrame**: Number of `<iframe>` elements.  
- **NoOfRedirects**: Number of redirects.  
- **HasSocialNet**: Indicates if the page has social media links.  
- **HasPasswordField**: Whether the page has a password input field.  

### **Target Variable**
- **Label:**  
  - `0 → Phishy`  
  - `1 → Legitimate`  

---

## 4. **Data Collection**
- The dataset used for this project was sourced from the **UCI Machine Learning Repository**.  
- It contains a combination of **URL metadata, web page features, and website behavior metrics** for phishing and legitimate URLs.  
- The dataset was downloaded in **CSV format** and used for further processing.
---

## 5. **Data Preprocessing - Data Cleaning**
1. **Loading and Cleaning Data:**  
   - Loaded the dataset using `pandas`.  
   - Examined missing values and duplicates.  
   - Applied **SimpleImputer** to fill missing values with the mean.  
   - Removed irrelevant features and duplicate entries.

---

## 6. **Exploratory Data Analysis (EDA)**

1. **Distribution Analysis:**  
   - Visualized the distribution of legitimate vs. phishing URLs.  
   - Examined feature distributions with histograms and box plots.  

2. **Outlier Detection & Treatment:**  
   - Identified outliers using **IQR** and **z-score** methods.  
   - Applied **outlier clipping** to reduce the influence of extreme values.  
   - Performed **Box-Cox** and **square transformations** to normalize skewed features and improve model stability.
     
3. **Correlation Analysis:**  
   - Calculated the **correlation matrix** to identify relationships between features.  
   - Visualized the matrix using a **heatmap** to detect multicollinearity.  
   - Removed or combined highly correlated features to reduce redundancy and prevent overfitting.  
     
## 7. **Split Data into Training and Testing Sets**
- Split the dataset into:
    X → Features
    y → Target variable (Label)
- Applied SMOTE (Synthetic Minority Over-sampling Technique) to balance the classes.
- Split the dataset into **80% training** and **20% testing** data.  
- Ensured **stratified splitting** to maintain class distribution.

---

## 8. **Feature Scaling**
- Standardized numerical features using **StandardScaler**.  
- Ensured consistent scaling across features to prevent magnitude bias.

---

## 9. **Feature Selection**
1. **Feature Importance Analysis:**  
   - Applied **SelectKBest** with `f_classif` scoring function.  
   - Selected the **24 most relevant features**.  
   - Ensured consistent feature names during transformations.  
   - Manually added the TLDLegitimateProb feature based on its **high custom score**, indicating strong predictive relevance.
   - Combined the 24 selected features with the manually added feature, resulting in **25 final features** used for model training.
---

## 10. **Model Building**
1. **Model Selection:**  
   - Trained multiple models to compare performance:  
     - **Logistic Regression**  
     - **SVM (Support Vector Machine)**  
     - **Random Forest**  
     - **Gradient Boosting**  
     - **XGBoost**  
     - **Decision Tree**  

---

## 11. **Model Evaluation**
1. **Evaluation Metrics:**  
   - **Accuracy:** Measures overall correctness.  
   - **Precision:** Measures true positives out of all predicted positives.  
   - **Recall:** Measures true positives out of actual positives.  
   - **F1 Score:** Harmonic mean of precision and recall.
- Found that Random Forest is the best-performing model, achieving near-perfect generalization with the highest accuracy, precision, and recall.

---

## 12. **Hyperparameter Tuning & Optimization**
1. **Random Forest Optimization:**  
   - Used **RandomizedSearchCV** for hyperparameter tuning to reduce execution time.  
   - Tuned parameters:  
     - `n_estimators`: Number of trees.  
     - `max_depth`: Limits tree depth to prevent overfitting.  
     - `min_samples_split`: Minimum samples required to split an internal node.  
     - `min_samples_leaf`: Minimum samples required for a leaf node.  
     - `max_features`: Number of features considered for the best split.  
     - `bootstrap`: Whether to use bootstrapping when building trees.  
   - **Best Parameters Found:**  
     ```python
     {'n_estimators': 150, 
      'min_samples_split': 2, 
      'min_samples_leaf': 1, 
      'max_features': 'log2', 
      'max_depth': 15, 
      'bootstrap': True}
     ```

2. **Final Model Performance:**  
   - **Accuracy:** 99.94%  
   - **Precision:** 99.91%  
   - **Recall:** 99.96%  
   - **F1 Score:** 99.94%  

---

---

## 13. **Save the Model**
1. Created a **scikit-learn pipeline** combining:  
   - **SimpleImputer** for missing values.  
   - **StandardScaler** for feature scaling.  
   - **RandomForestClassifier** with optimized hyperparameters.  
2. Saved the pipeline as a **.joblib** file for future predictions.

---

## 14. **Test with Unseen Data**
1. Applied the model to **unseen data samples**.  
2. Saved predictions along with features into a CSV file.  

---

## 15. **Interpretation of Results: Unseen Data Predictions Analysis**
1. Analyzed predictions with actual labels.  
2. Verified model performance on unseen data using metrics:  
   - **Accuracy:** 99.94%  
   - **Precision:** 99.91%  
   - **Recall:** 99.95%  
   - **F1 Score:** 99.93%  

---

## 16. **Future Work**
1. **Testing on Real-World Data:**  
   - Validate the model with real-world phishing datasets.  
   - Include additional **WHOIS data, DNS records, and website load times**.  

2. **Model Deployment:**  
   - Deploy the Django-based web app to a cloud platform (AWS or Heroku).  
   - Implement **continuous model improvement** with new training data.  

---

 **This project successfully demonstrates the effectiveness of machine learning in identifying phishing threats with high accuracy and real-time prediction capabilities.** 

