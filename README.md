# LLM-Powered Low-Code Data Annotation Platform

## Description
This project develops an AI-assisted platform that simplifies text data annotation using large language models (LLMs). The system automatically suggests labels for common NLP tasks (named entity recognition, text classification) and enables human validation/correction through an intuitive web interface. Designed for researchers and small teams without ML expertise.

## Clear Goals
1. Achieve **85%+ initial label accuracy** across 3 tasks: medical NER, product review sentiment, and legal document classification
2. Reduce average annotation time by **40%** compared to manual labeling
3. Support **5+ low-resource languages** through cross-lingual LLM prompting

## Data Collection
| Data Type | Source | Collection Method |
|-----------|--------|-------------------|
| Medical Texts | [MIMIC-III](https://physionet.org/content/mimiciii/1.4/) | Download de-identified clinical notes |
| Product Reviews | [Amazon Review Data (2018)](https://nijianmo.github.io/amazon/index.html) | Preprocessed subset download |
| Legal Contracts | [CUAD Dataset](https://www.atl.law.berkeley.edu/cuad-dataset/) | CC-BY licensed contract clauses |
| Low-Resource Texts | [FLORES-200](https://github.com/facebookresearch/flores) | Parallel sentences for 200 languages |

## Modeling Approach
1. **Core Architecture**:
   - LLM Suggestions: LLaMA-3-8B with dynamic few-shot prompting
   - Human-in-the-Loop: Active learning prioritizes uncertain samples
   - Quality Control: Snorkel framework for label reconciliation

2. **Key Techniques**:
   - Cross-lingual transfer learning for low-resource languages
   - Confidence calibration using temperature scaling
   - Rule-based post-processing with domain dictionaries

## Data Visualization
1. **Annotation Dashboard**:
   ```python
   # Sample visualization mockup
   def show_annotation_progress():
       return dcc.Graph(
           figure={
               'data': [
                   {'x': days, 'y': labeled_samples, 'name': 'Auto-Labeled'},
                   {'x': days, 'y': corrected_samples, 'name': 'Human-Validated'}
               ],
               'layout': {'title': 'Daily Labeling Productivity'}
           }
       )

## Test Plan
1. **Data Splitting**:

60% training

20% validation

20% held-out test
