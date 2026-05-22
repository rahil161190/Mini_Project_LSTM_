# 📰 LSTM News Summarizer (Inshorts-Inspired)

## 📌 Project Overview
This project demonstrates how to build an AI-powered news summarization model inspired by the **Inshorts app**, which delivers news in **60 words or less**.  
The objective is to use a **Recurrent Neural Network (RNN)** architecture to take a news article of **40–60 words** and generate a concise summary of **under 30 words**.

---

## ⚙️ Dependencies and Libraries
- **TensorFlow / Keras**: Sequence-to-sequence model layers (LSTM, Embedding, Dense, TimeDistributed)  
- **NLP Tools**: `nltk`, `spaCy`, `rouge-score` for text processing and evaluation  
- **Data Handling & Visualization**: `pandas`, `numpy`, `matplotlib`, `seaborn`

---

## 📂 Dataset and Preprocessing
Datasets: `news_summary.csv` and `news_summary_more.csv`

Steps:
- **Text Cleaning**: Regex removes non-alphabetic characters, multiple spaces, HTML tags, and unnecessary punctuation  
- **Start/End Tokens**: Summaries wrapped with `sostok` (start) and `eostok` (end)  
- **Vocabulary Optimization**: Keras Tokenizer converts text to integer sequences; rare words (<5 occurrences) removed  
  - ~64% of text vocabulary and ~66% of summary vocabulary filtered out  
- **Padding**: Sequences padded with zeros (`padding='post'`)  
- **Train/Test Split**: 10% of data allocated for validation

---

## 🏗️ Model Architecture
- **Architecture**: Encoder–Decoder with LSTM  
- **Trainable Parameters**: 11,465,982  
- **Hyperparameters**: Latent dimension = 300, Embedding dimension = 200  

### 🔹 Encoder
- Embedding layer  
- Three stacked LSTM layers  
- Dropout = 0.4, Recurrent Dropout = 0.4  

### 🔹 Decoder
- Embedding layer  
- Single LSTM layer (Dropout = 0.4, Recurrent Dropout = 0.2)  
- Takes initial states from final Encoder layer  

### 🔹 Output Layer
- TimeDistributed Dense layer  
- Softmax activation → word probability distribution

---

## 🎯 Training and Performance
- **Compilation**: Adam optimizer, `sparse_categorical_crossentropy` loss  
- **Training Parameters**: 20 epochs, batch size = 1024  
- **Callbacks**:  
  - EarlyStopping (patience = 10, monitor = validation loss)  
  - ModelCheckpoint (save best weights)  

### 📊 Results
- Validation Loss: **2.0870**  
- Validation Accuracy: **71.10%** (by epoch 20)

---
