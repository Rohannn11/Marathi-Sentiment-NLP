# MarathiSentimentNLP

A sentiment classification project for Marathi social media comments. The system combines preprocessing tailored for Marathi’s linguistic richness with modern NLP models to classify text into positive, negative, or neutral sentiment.  

---

## Overview
This project addresses the challenges of analyzing **code-mixed, noisy, and morphologically rich Marathi text** from social media. We experiment with both traditional and transformer-based approaches to evaluate trade-offs in performance and efficiency.  

---

## Pipeline

### 1. Preprocessing
- **Libraries used:**  
  - **Indic NLP Library**:  
    - Tokenization  
    - Root word extraction (using Morfessor models)  
    - Handling Marathi inflections  
  - **NLTK (Natural Language Toolkit):** Stopword handling, token manipulation  
  - **Regex (re):** Cleaning noisy patterns (emojis, hashtags, punctuation)  

- **Purpose:** Normalize and prepare Marathi (and code-mixed English-Marathi) data for modeling.  

---

### 2. Feature Representation
- **FastText (Baseline Approach):**  
  - Subword-level skip-gram training  
  - Handles out-of-vocabulary (OOV) words via character n-grams  
  - Produces **static embeddings** (one vector per word)  

- **MahaBERT (Transformer Approach):**  
  - Pretrained on 752M Marathi tokens  
  - Produces **contextual embeddings** (word meaning changes by context)  
  - Fine-tuned with **LoRA (Low-Rank Adaptation)** for efficient adaptation  

---

### 3. Model Training
- **LoRA Fine-Tuning:**  
  - Updates only a small fraction of parameters (~2.78%)  
  - Prevents catastrophic forgetting of pretrained knowledge  
  - Memory-efficient and fast to train  

- **Training Strategy:**  
  - Batch size optimized for GPU memory  
  - Learning rate scheduling (different for BERT layers vs classification head)  
  - Early stopping to prevent overfitting  

---

### 4. Evaluation
- **Metrics used:**  
  - Accuracy (baseline)  
  - F1-score (better for imbalanced datasets)  
  - Precision and Recall trade-offs  

- **Why multiple metrics?**  
  Social media sentiment data is often imbalanced; accuracy alone can be misleading.  

---

### 5. Deployment Strategy
- Export fine-tuned model with LoRA adapters  
- Lightweight deployment (merge adapters with base model when needed)  
- Extendable to other domains (e.g., financial sentiment in Marathi) by training separate adapters  

---

## Key Takeaways
- Indic NLP + NLTK + Regex ensure clean inputs for modeling  
- FastText offers efficient baseline embeddings  
- MahaBERT with LoRA achieves state-of-the-art results for Marathi sentiment analysis  
- Multi-metric evaluation provides fairer assessment on imbalanced datasets  

---

## License
This project is licensed under the **MIT License**.  
