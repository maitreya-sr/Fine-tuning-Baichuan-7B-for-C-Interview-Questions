# Research Report: Fine-tuning Baichuan-7B for C++ Interview Questions

## Project Description
This project focuses on adapting the Baichuan-7B large language model for industry-specific applications, specifically in the domain of C++ interview questions. The goal is to improve the model's ability to generate accurate and professional responses to C++ technical queries through fine-tuning.

## Preliminary Data Visualization
The dataset consists of 1067 C++ interview questions and answers, sourced from online interview experiences and GPT-4-generated content. The dataset is divided as follows:
- **Training Set**: 1028 examples
- **Test Set**: 39 examples

A histogram of question lengths in the dataset reveals a relatively uniform distribution, with most questions ranging between 10 and 50 words. Additionally, word frequency analysis highlights key technical terms such as "pointer," "memory," "inheritance," and "overloading."

## Data Processing Details
The data processing steps completed so far include:
1. **Data Cleaning**: Removed duplicate and incomplete questions.
2. **Tokenization**: Applied subword tokenization to ensure compatibility with the Baichuan-7B tokenizer.
3. **Normalization**: Standardized text formatting, such as converting all characters to lowercase and removing extraneous punctuation.
4. **Dataset Splitting**: Ensured a meaningful test set by selecting diverse questions representative of different C++ topics.

## Modeling Methods Used So Far
We used **LoRA (Low-Rank Adaptation)** for efficient fine-tuning of the Baichuan-7B model. Training was conducted over **25 epochs** until convergence. The training methodology involved:
- **Loss Function**: Cross-entropy loss for supervised fine-tuning.
- **Optimizer**: AdamW with a learning rate scheduler.
- **Evaluation Metrics**: BLEU-4, ROUGE-1, ROUGE-2, and ROUGE-L scores to assess response similarity with ground truth answers.

## Preliminary Results
- **Metric Improvements**:
  - BLEU-4 increased from **21.25** to **26.31** (+23%)
  - ROUGE-1 increased from **46.67** to **50.96** (+9%)
  - ROUGE-2 increased from **22.37** to **26.51** (+19%)
  - ROUGE-L increased from **32.41** to **35.54** (+10%)

- **Qualitative Observations**:
  - The pre-trained model exhibited repetition and irrelevant outputs for technical questions.
  - After fine-tuning, the model provided more structured, relevant, and accurate answers.
  - Compared to human responses (e.g., from Zhihu discussions), the fine-tuned model demonstrated improved coherence and correctness.

## Next Steps
Moving forward, we plan to:
1. Conduct further hyperparameter tuning to refine model performance.
2. Introduce additional domain-specific datasets for broader generalization.
3. Deploy the model in an interactive system for real-world evaluation.

These steps will help validate the effectiveness of our fine-tuning approach and further optimize the model for industry-specific applications.
