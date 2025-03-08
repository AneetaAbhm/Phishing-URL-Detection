# PHISHING URL DETECTION - PHASE 2
## 1.Overview of Problem Statement:

Phishing attacks are one of the most common cyber threats, costing individuals and organizations billions annually. Attackers use deceptive URLs to steal sensitive information like passwords, credit card details, and personal data. Traditional methods of detecting phishing URLs (e.g., blacklists) are reactive and fail to catch new threats. This project aims to build a proactive phishing detection system using machine learning to analyze URL features and classify them as malicious or safe.

## 2. Objective:

Develop a machine learning model to classify URLs as phishing or legitimate based on features extracted from the URL and its metadata. The goal is to create a robust system that can detect phishing attempts in real-time, protecting users from cyber threats.

## 3. Data Description
This dataset contains multiple features extracted from URLs, their content, and web page behavior to help classify URLs as either **legitimate** or **phishing**. Below is a detailed explanation of each feature:

### URL & Domain-Based Features
- **FILENAME**: Name of the file containing the dataset entry.  
- **URL**: The full web address being analyzed.  
- **URLLength**: Total length of the URL (longer URLs may be suspicious).  
- **Domain**: The main domain of the URL (e.g., example.com).  
- **DomainLength**: Length of the domain (long domains can indicate phishing).  
- **IsDomainIP**: Whether the domain is an IP address (1 = Yes, 0 = No).  
- **TLD**: The top-level domain (e.g., .com, .org, .xyz).  
- **TLDLegitimateProb**: Probability of the TLD being legitimate based on past data.  

### Character-Based Features
- **URLSimilarityIndex**: Similarity score with known trusted URLs.  
- **CharContinuationRate**: Measures repeated character patterns in the URL.  
- **URLCharProb**: Probability distribution of characters in the URL.  
- **TLDLength**: Length of the top-level domain.  
- **NoOfSubDomain**: Number of subdomains (more subdomains can indicate phishing).  
- **HasObfuscation**: Whether the URL contains obfuscation techniques (1 = Yes).  
- **NoOfObfuscatedChar**: Number of obfuscated characters in the URL.  
- **ObfuscationRatio**: Ratio of obfuscated characters to total URL length.  
- **NoOfLettersInURL**: Count of alphabetic characters in the URL.  
- **LetterRatioInURL**: Ratio of letters to the total URL length.  
- **NoOfDigitsInURL**: Number of numeric digits in the URL.  
- **DigitRatioInURL**: Ratio of numeric digits to the total URL length.  
- **NoOfEqualsInURL**: Number of '=' characters in the URL (used in tracking links).  
- **NoOfQMarkInURL**: Number of '?' characters (common in phishing).  
- **NoOfAmpersandInURL**: Number of '&' characters in the URL.  
- **NoOfOtherSpecialCharsInURL**: Count of other special characters (@, %, etc.).  
- **SpecialCharRatioInURL**: Ratio of special characters to total URL length.  

### Security & HTTPS Features
- **IsHTTPS**: Whether the URL uses HTTPS (1 = Yes, 0 = No).  

### Web Page Content Features
- **LineOfCode**: Number of lines in the HTML source code.  
- **LargestLineLength**: Length of the longest line in the source code.  
- **HasTitle**: Whether the web page has a `<title>` tag (1 = Yes).  
- **Title**: The text inside the `<title>` tag.  
- **DomainTitleMatchScore**: Similarity score between domain name and page title.  
- **URLTitleMatchScore**: Similarity score between URL and page title.  
- **HasFavicon**: Whether the page has a favicon (1 = Yes).  

### Website Behavior Features
- **Robots**: Whether the website has a `robots.txt` file (1 = Yes).  
- **IsResponsive**: Whether the website is mobile-responsive (1 = Yes).  
- **NoOfURLRedirect**: Number of times the URL redirects.  
- **NoOfSelfRedirect**: Number of self-redirects within the same domain.  

### Social & Interactive Features
- **HasDescription**: Whether the page has a meta description (1 = Yes).  
- **NoOfPopup**: Number of pop-ups on the website.  
- **NoOfiFrame**: Number of `<iframe>` elements (often used in phishing).  
- **HasExternalFormSubmit**: Whether the page submits data to an external domain.  
- **HasSocialNet**: Whether the page contains social media links.  
- **HasSubmitButton**: Whether the page has a submit button (1 = Yes).  
- **HasHiddenFields**: Whether the page contains hidden form fields.  
- **HasPasswordField**: Whether the page has an input field for passwords.  

### Financial & Phishing Keywords
- **Bank**: Whether the URL contains bank-related words (1 = Yes).  
- **Pay**: Whether the URL contains payment-related words (1 = Yes).  
- **Crypto**: Whether the URL contains cryptocurrency-related words (1 = Yes).  

### Multimedia & External Links
- **HasCopyrightInfo**: Whether the page has copyright information.  
- **NoOfImage**: Number of images on the webpage.  
- **NoOfCSS**: Number of CSS files linked in the HTML.  
- **NoOfJS**: Number of JavaScript files linked in the HTML.  
- **NoOfSelfRef**: Number of self-referencing links in the HTML.  
- **NoOfEmptyRef**: Number of empty or broken links.  
- **NoOfExternalRef**: Number of links pointing to external domains.  

### Target Variable
- **label**: The classification of the URL:  
  - **1 → Legitimate**  
  - **0 → Phishing**

---
## Usage Instructions
1. Load the dataset using `pandas`.  
2. Perform data preprocessing, including handling missing values, outlier removal, and feature scaling.  
3. Conduct Exploratory Data Analysis (EDA) to identify key insights.  
4. Apply feature engineering and selection techniques.  
5. Split the dataset into train and test data.
---

