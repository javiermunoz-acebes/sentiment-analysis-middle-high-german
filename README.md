# Sentiment Analysis for Middle High German Literature

Hybrid sentiment analysis for Middle High German (MHG) literary texts using the SentiMHD lexicon. This repository contains reproducible computational methods for detecting emotions and sentiment polarity in medieval German literature, with a focus on Wolfram von Eschenbach's *Parzival*.

## Project Overview

This project implements three complementary approaches to sentiment analysis in MHG texts:

1. **Lexicon-based approach**: Direct matching against the SentiMHD expert dictionary
2. **Supervised Machine Learning**: Logistic regression with TF-IDF features trained on manually annotated corpus
3. **Rule-based hybrid system**: Deterministic analysis combining lexical matching, contextual patterns, and negation handling

The methods are evaluated against a gold standard corpus of manually annotated verses, achieving up to 84.21% accuracy with substantial inter-annotator agreement (Cohen's κ=0.696).

## Repository Contents

### Data Files

- **`Parzival_MHD.csv`**: Complete text of *Parzival* Chapter XVI (1229 verses) in CSV format, one verse per line
- **`Parzival_XVI_gold_standard`**: Gold standard corpus with manual sentiment annotations (POSITIV, NEGATIV, NEUTRO, MIX) and annotation type classification (LEX, CONTEXT, BODY, SENS, PROCESS)
- **`Sentimhd.txt`**: SentiMHD sentiment lexicon for Middle High German (526 lemmas, 1486 variant forms)

### Notebooks

- **`Parzival_Sentimhd.ipynb`**: Main analysis notebook implementing all three approaches with detailed documentation, visualization, and evaluation metrics

### Lexicon

The **SentiMHD** dictionary is a specialized sentiment lexicon for Middle High German developed by Friedrich Michael Dimpel. It contains expert-annotated positive and negative terms with morphological variants covering courtly, theological, and emotional vocabulary from 12th-16th century German literature.

**Citation**:
> Dimpel, Friedrich Michael (2023). *SentiMhd – ein Sentiment-Wörterbuch für das Mittelhochdeutsche*. DARIAH-DE.  
> https://doi.org/10.20375/0000-0010-05bd-4

## Methodology

### 1. Lexicon-Based Analysis

Direct token matching against SentiMHD variants to calculate polarity density per verse:
- Proportion of positive words
- Proportion of negative words  
- Proportion of neutral words

### 2. Supervised Machine Learning

Logistic regression classifier with:
- **TF-IDF vectorization**: Unigrams and bigrams (max 5000 features)
- **Class balancing**: Weighted classes to handle imbalanced annotations
- **Cross-validation**: 5-fold stratified evaluation
- **Hybrid features**: TF-IDF + lexicon-based proportions (combined sparse matrices)

### 3. Rule-Based Hybrid System

Three-level decision hierarchy:

**Level 1**: Lexical detection of explicit affect terms (expanded vocabulary including courtly/theological concepts: *triuwe*, *minne*, *êre*, *jâmer*, *nôt*, *kumber*)

**Level 2**: Contextual pattern rules for implicit negativity:
- Death references (*tôt*, *sterben*)
- Rhetorical lament questions (*wie lange sol*, *waz toug ich*)
- Hypothetical negative constructions (*wirt... verlorn*)

**Level 3**: Negation handling with polarity inversion (proximity-based: ±3 tokens from positive terms)



