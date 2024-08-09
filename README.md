# Siamese Network for Quora Question Pair Similarity

This repository contains the implementation of a Siamese Network model for identifying whether two questions from the Quora dataset are semantically similar. The model uses a deep learning architecture with Triplet Loss to achieve this task.

## Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Model Architecture](#model-architecture)
- [Training](#training)
- [Evaluation](#evaluation)
- [Results](#results)

## Project Overview

The goal of this project is to build a Siamese Network that can predict whether two questions are duplicates. The Siamese Network architecture is particularly well-suited for tasks where pairs of inputs need to be compared, such as signature verification, face recognition, and, in this case, question similarity.

## Dataset

The dataset used in this project is the Quora Question Pairs dataset. It contains over 400,000 pairs of questions, along with a label indicating whether the pair of questions are duplicates.

- **Number of Question Pairs:** 404,351
- **Columns:**
  - `qid1`: Unique ID for the first question.
  - `qid2`: Unique ID for the second question.
  - `question1`: Text of the first question.
  - `question2`: Text of the second question.
  - `is_duplicate`: Label indicating whether the questions are duplicates (1) or not (0).

## Model Architecture

The model is a Siamese Network built using TensorFlow and Keras. The network consists of two identical sub-networks (sister networks) with shared weights. Each sub-network is composed of the following layers:

1. **Text Vectorization Layer:** Converts text input into integer sequences.
2. **Embedding Layer:** Maps the integer sequences to dense vectors.
3. **LSTM Layer:** Processes the sequences and captures contextual information.
4. **Global Average Pooling Layer:** Reduces the output dimensions from the LSTM layer.
5. **Normalization Layer:** Normalizes the output vectors.

The outputs of the two sub-networks are then concatenated and passed through a cosine similarity function to determine the similarity score.

### Loss Function

The model uses **Triplet Loss** with **Negative Hard Mining** to minimize the distance between similar question pairs and maximize the distance between dissimilar ones.

## Training

The dataset was split into training, validation, and test sets:

- **Training Set:** 300,000 pairs
- **Test Set:** 10,240 pairs
- **Validation Set:** Split from the training set (20% of training data)

The model was trained for 2 epochs with a batch size of 256. The Adam optimizer was used with a learning rate of 0.0001.

## Evaluation

The model was evaluated using the following metrics:

- **Accuracy:** 73.5%
- **Precision:** 0.69
- **Recall:** 0.85
- **Confusion Matrix:** The model shows a balance between false positives and false negatives but tends to incorrectly predict dissimilar pairs as similar.

## Results

The model performed reasonably well, with an accuracy of approximately 73.5%. However, there is room for improvement, particularly in reducing the false positive rate.

### Examples of Predictions:

1. **Question 1:** "When will I see you?"  
   **Question 2:** "When can I see you again?"  
   **Cosine Similarity:** 0.8874  
   **Result:** [True]

2. **Question 1:** "What city is the capital of USA?"  
   **Question 2:** "What is the US capital?"  
   **Cosine Similarity:** 0.6917  
   **Result:** [True]

3. **Question 1:** "Do you enjoy reading books in the free time?"  
   **Question 2:** "Do you like to read novels when you have spare time?"  
   **Cosine Similarity:** 0.6748  
   **Result:** [True]

---

Feel free to customize this README further to suit your specific needs!
