# Social Media Engagement Text Processing Analysis

This repository contains a comprehensive text processing analysis of social media engagement data, specifically focusing on Instagram-style posts with media captions and user comments.

## Dataset
- **Source**: `data/raw/engagements.csv`
- **Content**: Social media engagement data with media captions and user comments
- **Size**: 17,841 records (after removing null values)
- **Columns Analyzed**: 
  - `media_caption`: Instagram-style post captions
  - `comment_text`: User comments on posts

## Notebook: `notebooks/text_processing.ipynb`

This Jupyter notebook performs comprehensive natural language processing (NLP) analysis on social media engagement data using spaCy and TextBlob.

### Key Features

#### 1. **Data Preprocessing**
- Loads engagement data from CSV
- Handles missing values (11 nulls in media_caption, 29 in comment_text)
- Removes null records and resets index

#### 2. **Parts of Speech (POS) Tagging**
- Uses spaCy's `en_core_web_sm` model for POS tagging
- Analyzes both media captions and comment text
- Extracts grammatical structure information
- Creates frequency distributions and comparisons
- Generates visualizations comparing POS usage between captions and comments

#### 3. **Named Entity Recognition (NER)**
- Identifies and extracts named entities from both text types
- Categorizes entities by type (PERSON, ORG, GPE, PRODUCT, etc.)
- Provides comprehensive statistics on entity frequency
- Creates visualizations showing entity type distributions
- Demonstrates the `named_entity_recognizer` function

#### 4. **Sentiment Analysis**
- Uses TextBlob for sentiment analysis of both media captions and user comments
- Categorizes sentiments into 5 categories:
  - Very Negative (≤ -0.6)
  - Negative (-0.6 to -0.15)
  - Neutral (-0.15 to 0.15)
  - Positive (0.15 to 0.6)
  - Very Positive (> 0.6)
- Provides both categorical and numerical polarity scores
- Creates comprehensive visualizations and statistics
- **Comparative Analysis**: Direct comparison between media caption and comment sentiment
- **Correlation Analysis**: Examines relationship between caption and comment sentiment

#### 5. **Data Export**
- Saves processed dataframe to `data/interim/processed_engagements_with_sentiment.csv`
- Includes all original data plus new analysis columns
- **New Columns Added**:
  - POS tagging: `media_caption_pos`, `comment_text_pos`
  - Named entities: `media_caption_ner`, `comment_text_ner`
  - Sentiment analysis: `comment_sentiment`, `comment_polarity`, `media_caption_sentiment`, `media_caption_polarity`
  - Length analysis: `comment_length`, `media_caption_length`

#### 6. **Analysis Outputs**
- **POS Analysis**: 17 unique POS tags identified, 1.4M+ tokens processed
- **NER Analysis**: Identifies brands, people, locations, and other entities
- **Sentiment Analysis**: 
  - Comments: 87.4% neutral, 11.3% positive, 1.4% negative
  - Media captions: Comparative sentiment analysis with comments
- **Visualizations**: Multiple chart types including bar charts, pie charts, histograms
- **Pattern Analysis**: Sentiment by text length, entity density, correlation analysis

### Technical Stack
- **Python Libraries**: pandas, numpy, matplotlib, spacy, textblob
- **NLP Models**: spaCy English model (en_core_web_sm)
- **Data Processing**: Text preprocessing, tokenization, entity extraction
- **Visualization**: Matplotlib for comprehensive data visualization

### Key Insights
- Media captions contain more diverse vocabulary and longer text
- Comments are generally short and neutral in sentiment
- Media captions tend to be more positive than user comments
- Named entities help identify key brands, people, and locations mentioned
- POS tagging reveals grammatical patterns in social media communication
- Sentiment analysis shows overall positive engagement with some negative feedback
- Correlation analysis reveals relationships between caption and comment sentiment

### Output Files
- **Processed Data**: `data/interim/processed_engagements_with_sentiment.csv`
  - Complete dataset with all NLP analysis results
  - Ready for further analysis or machine learning modeling
  - Includes sentiment scores, POS tags, named entities, and text length metrics

This analysis provides valuable insights into social media engagement patterns, user sentiment, and content characteristics that can inform marketing and content strategy decisions.

## Notebook: `notebooks/decision_trees.ipynb`

This Jupyter notebook implements machine learning models using decision trees to predict comment sentiment based on media caption features and named entity recognition results.

### Key Features

#### 1. **Data Preparation for Modeling**
- Loads processed engagement data from `data/interim/processed_engagements_with_sentiment.csv`
- Filters data to include only records with clear sentiment labels (very positive, positive, negative, very negative)
- Creates binary sentiment classification: `positive` (1 for positive/very positive, 0 for negative/very negative)
- Extracts NER features as binary indicators:
  - `has_gpe`: Geographic/political entities (17.71% of records)
  - `has_norp`: Nationalities/religious/political groups (6.35% of records)  
  - `has_person`: Person names (40.97% of records)
  - `has_org`: Organizations (40.52% of records)

#### 2. **Feature Engineering**
- Combines sentiment features with NER features for modeling
- Uses `media_caption_polarity` (TextBlob sentiment score) as primary predictor
- Creates binary indicators from named entity recognition results
- Prepares data in format suitable for scikit-learn models

#### 3. **Data Splitting**
- Implements train/validation/test split (60/20/20)
- Uses stratified splitting with random state for reproducibility
- Separates features from target variable (`positive` sentiment)

#### 4. **Decision Tree Modeling**
- Implements DecisionTreeClassifier from scikit-learn
- Uses DictVectorizer for feature encoding
- Evaluates model performance using ROC-AUC score
- Performs hyperparameter tuning for optimal performance

#### 5. **Hyperparameter Optimization**
- Tests different `max_depth` values (1, 2, 3, 4, None)
- Optimizes `min_samples_leaf` parameter (1, 5, 10, 15, 20, 100, 200, 500)
- Uses validation set to prevent overfitting
- Creates heatmap visualization of parameter combinations

#### 6. **Model Interpretation**
- Uses `export_text()` to visualize decision tree structure
- Identifies key decision rules and feature importance
- Shows how model makes predictions based on feature thresholds

### Technical Implementation
- **Libraries**: scikit-learn, pandas, numpy, matplotlib, seaborn
- **Evaluation Metric**: ROC-AUC score for binary classification
- **Feature Processing**: DictVectorizer for categorical encoding
- **Model**: DecisionTreeClassifier with optimized parameters

### Key Results
- **Best Model**: max_depth=3, min_samples_leaf=200 (optimal balance of performance and generalization)
- **Primary Predictor**: `media_caption_polarity` is the most important feature
- **NER Impact**: Geographic entities (`has_gpe`) provide additional predictive value
- **Model Performance**: Achieves reasonable performance while avoiding overfitting

### Model Insights
- Media caption sentiment is the strongest predictor of comment sentiment
- Geographic mentions in captions provide additional predictive power
- Deeper trees (>3 levels) show diminishing returns due to overfitting
- Minimum sample leaf size of 200 provides good generalization

This modeling approach demonstrates how to build interpretable machine learning models for sentiment prediction using both content features and entity recognition results.