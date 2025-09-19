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