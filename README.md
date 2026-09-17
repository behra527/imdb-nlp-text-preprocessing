# IMDb NLP Text Preprocessing

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![NLTK](https://img.shields.io/badge/NLTK-3.9.1-green)
![Pandas](https://img.shields.io/badge/Pandas-2.2.3-blue?logo=pandas)
![Google Colab](https://img.shields.io/badge/Google%20Colab-Notebook-orange?logo=googlecolab)
![NLP](https://img.shields.io/badge/NLP-Text%20Preprocessing-purple)

A Natural Language Processing project focused on preprocessing IMDb movie reviews using **NLTK** and **Python**.

The project covers sentence tokenization, word tokenization, noise removal, lowercasing, standard stopword removal, sentiment-aware stopword handling, and before/after text analysis.

## Project Overview

Text preprocessing is an important step in NLP because raw text often contains HTML tags, inconsistent capitalization, punctuation, extra whitespace, and unnecessary words.

In this project, a modular preprocessing pipeline was developed for IMDb movie reviews while specifically protecting sentiment-important negation words such as `not`.

## Dataset

The project uses the **IMDb Movie Reviews Dataset**.

Original dataset:

* 50,000 movie reviews
* 25,000 positive reviews
* 25,000 negative reviews
* Columns: `review`, `sentiment`
* 418 duplicate rows
* No missing values

A balanced development subset of **1,000 reviews** was used for preprocessing development and evaluation:

* 500 positive
* 500 negative

## Technologies Used

* Python
* Google Colab
* Pandas
* NLTK
* Regular Expressions (`re`)

## Project Workflow

The preprocessing workflow follows these steps:

1. Dataset Loading
2. Development Dataset Selection
3. Baseline Text Inspection
4. Noise Removal
5. Lowercasing
6. Sentence Tokenization
7. Word Tokenization
8. Standard Stopword Analysis
9. Sentiment-Aware Stopword Removal
10. Modular Preprocessing Pipeline
11. Clean Text Representation
12. Before vs. After Analysis
13. Vocabulary Analysis
14. Token Reduction Analysis
15. Quality Assurance

## Preprocessing Pipeline

The main preprocessing pipeline performs:

```text
Raw Review
    ↓
Remove HTML / Noise
    ↓
Lowercase
    ↓
Word Tokenization
    ↓
Sentiment-Aware Stopword Removal
    ↓
Clean Tokens
    ↓
Clean Text
```

### Noise Removal

HTML tags and unnecessary whitespace are removed from reviews.

Example:

```text
<br />This movie was GREAT!
```

becomes:

```text
This movie was GREAT!
```

### Lowercasing

Text is converted into a consistent lowercase representation.

```text
STREET FIGHTER
```

becomes:

```text
street fighter
```

### Sentence Tokenization

NLTK `sent_tokenize()` is used to divide a review into individual sentences.

### Word Tokenization

NLTK `word_tokenize()` converts text into individual tokens.

Example:

```text
This movie is not good.
```

becomes:

```python
['this', 'movie', 'is', 'not', 'good', '.']
```

## Sentiment-Aware Stopword Removal

Standard stopword removal can remove important negation words such as `not`.

For example:

```text
This movie is not good.
```

If `not` is removed:

```text
movie good
```

The original meaning can be changed.

Therefore, a custom stopword configuration was created to preserve sentiment-related negation words.

Protected examples include:

```text
not
no
nor
never
isn't
wasn't
don't
didn't
doesn't
can't
couldn't
won't
wouldn't
shouldn't
```

NLTK tokenization can split contractions such as:

```text
don't
```

into:

```text
do + n't
```

The negation signal is therefore retained during preprocessing.

## Modular Pipeline

The project uses reusable preprocessing functions instead of placing all operations in one large code block.

Main functions include:

```python
remove_noise()
normalize_text()
remove_stopwords()
tokenize_sentences()
preprocess_text()
preprocess_text_with_sentences()
```

This makes the preprocessing workflow easier to understand, test, reuse, and extend.

## Results

The following results were obtained from the **1,000-review development subset**.

### Token Analysis

| Metric          |  Result |
| --------------- | ------: |
| Raw tokens      | 274,114 |
| Clean tokens    | 153,045 |
| Tokens removed  | 121,069 |
| Token reduction |  44.17% |

### Vocabulary Analysis

| Metric                | Result |
| --------------------- | -----: |
| Raw vocabulary        | 20,103 |
| Clean vocabulary      | 19,206 |
| Unique tokens removed |    897 |
| Vocabulary reduction  |  4.46% |

The difference between token reduction and vocabulary reduction is expected. Frequent stopwords can occur many times in the dataset, reducing the total number of token occurrences substantially while having a smaller effect on the number of unique words.

## Quality Assurance

The preprocessing pipeline was tested after implementation.

Results:

* Total reviews processed: 1,000
* Empty cleaned token lists: 0
* Missing clean text: 0
* Positive reviews: 500
* Negative reviews: 500

Negation preservation was also tested:

```text
This movie is not good.
```

Output:

```python
['movie', 'not', 'good', '.']
```

This confirmed that the important negation word `not` was preserved.

## Key Findings

* Sentence tokenization separates reviews into individual sentences.
* Word tokenization converts reviews into individual tokens.
* HTML and whitespace noise can be removed using regular expressions.
* Lowercasing creates a consistent text representation.
* Standard stopword removal can remove sentiment-important negation.
* A sentiment-aware stopword list helps preserve important negation signals.
* Total token occurrences were reduced by **44.17%**.
* Unique vocabulary was reduced by **4.46%**.
* QA confirmed that all 1,000 development reviews produced valid cleaned outputs.

## Future Improvements

Possible extensions include:

* Stemming
* Lemmatization
* Punctuation handling
* Contraction normalization
* TF-IDF feature extraction
* Bag-of-Words representation
* Sentiment classification
* Word embeddings
* Transformer-based text preprocessing

## Conclusion

This project developed a modular NLP preprocessing pipeline for IMDb movie reviews.

The pipeline combines noise removal, lowercasing, sentence tokenization, word tokenization, and sentiment-aware stopword removal. The analysis demonstrated a substantial reduction in token occurrences while preserving most of the unique vocabulary.

The resulting preprocessing pipeline can be used as a foundation for downstream NLP tasks such as sentiment analysis, text classification, and feature extraction.
