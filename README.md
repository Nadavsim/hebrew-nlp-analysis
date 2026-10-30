
# Modern vs. Historical Hebrew: An NLP Analysis

## Overview
This repository contains a comprehensive Natural Language Processing (NLP) research project investigating the historical linguistic roots of Modern Israeli Hebrew. 

The primary research question is the hypothesis proposed by Prof. Edith Doron, which suggests that Modern Hebrew is closer in structure to Biblical Hebrew. Through deep computational analysis of morphology, syntax, and lexicon, this project tests whether Modern Hebrew is effectively a continuation of Biblical Hebrew, or if its deep syntactic "skeleton" actually stems from Rabbinic/Mishnaic Hebrew.

## Architecture & Features
The codebase is built in Python and relies heavily on **DictaBERT** (`dicta-il/dictabert-tiny-joint`) for high-accuracy morphological tagging and dependency parsing of Hebrew text.

### 1. Linguistic Feature Extraction
The pipeline breaks down Hebrew sentences into multiple structural "lenses":
* **Lexical Signatures:** Tracking top-50 word frequencies and specific historical markers.
* **Morphology & POS:** Analyzing the distribution of Parts of Speech, gender, number, person, and tense.
* **Syntax & Dependency:** Calculating Syntactic Tree Depth, Clausal Word Order (V1 vs. V2), and Dependency Relations.
* **Historical Markers:** Infinitive vs. Gerund usage, and Possessive Constructions (Construct-State/Smixut vs. Prepositional/Shel).

### 2. Statistical Distance Metrics
To mathematically prove linguistic proximity, the project calculates multiple similarity/distance metrics across all corpora:
* Manhattan & Euclidean Distances
* Cosine Similarity
* Jaccard & Dice Similarities
* Jensen-Shannon (JS) Divergence 

### 3. Machine Learning Classifier
A robust `LogisticRegression` pipeline (evaluated using 10-Fold Cross Validation) trained to classify text as either Biblical (0) or Rabbinic (1). It tests Modern Hebrew genres (news, blogs, medical, literary) across 5 independent models:
1. **Lexical:** Raw vocabulary.
2. **Morph:** Inflection patterns.
3. **Syntax:** Dependency edges and distances.
4. **Structure:** Abstract POS sequencing.
5. **Linguistic:** Custom mathematical heuristics (Tree depth, unique word ratios, V1/V2 scores).

## Installation & Setup

```bash
# 1) Clone the repository
git clone https://github.com/Nadavsim/hebrew-nlp-analysis.git
cd hebrew-nlp-analysis

# 2) Create & activate a virtual environment (recommended)
python -m venv .venv
# Windows
.\.venv\Scriptsctivate
# macOS/Linux
# source .venv/bin/activate

# 3) Install dependencies
pip install -r requirements.txt

# 4) Add the input files into the relevant sub-folders

# 5) Run the example
python main.py
# Menu options:
#   1. Load File: copy text/XML files into the target directories.
#   2. Run Analysis: process raw texts through DictaBERT and generate base JSON tokens.
#   3. Print Statistics: extract linguistic features, plot Matplotlib bar charts, generate the
#      Similarity Distance CSV, and run the ML classifier on the Modern Hebrew datasets.
#      Available only after a file was analyzed.

# 6) Run the classifier
python classifier.py
# Menu options:
#   1. Run modern analysis: runs all Modern Hebrew datasets through the trained classifier and
#      prints the percentage of "Rabbinic" vs. "Biblical" alignment per genre, for all 5 lenses.
#   2. Manual analysis: paste any Hebrew sentence; it is parsed with DictaBERT and all 5 trained
#      models classify it as "Biblical" or "Rabbinic" with a confidence score each.
```

## Authors
University NLP mini-project, built as a pair by Nadav Simchai and [Shai2312](https://github.com/Shai2312). The original repository is [Shai2312/NPL-mini-project](https://github.com/Shai2312/NPL-mini-project).
