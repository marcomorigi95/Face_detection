# Face Detection

## Run the Project in Google Colab

Click the badge below to open the notebook directly in Google Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Y96isILWmU5u9Kv88Qq_UkJVSyLr-nUG?usp=sharing)

---


# Face Detection System

**Project Goal:**
This project aims to develop a **lightweight, non-deep learning face detection system** that helps photography technicians **optimize settings for selfies** — whether it’s one person or a group.

---

## Why No Deep Learning?

Due to **limited computing resources**, this project does **not** use any pre-trained models or deep learning approaches. Instead, it leverages traditional computer vision techniques to deliver a **computationally efficient**, yet effective solution for face detection.

---

## Method Overview

The system follows a structured pipeline built entirely from scratch. Below are the main stages of the process, all implemented and explained in detail in the notebook:

### 1. Dataset Creation

* **Positive Class:** Pre-collected dataset of face images (no need for more collection).
* **Negative Class:** Instead of collecting a massive dataset, we:

  * Use fewer than 1,000 non-face images.
  * Extract multiple small patches from each image.
  * Ensure that **patches match the size** of positive samples.
  * This strategy increases negative variety while remaining resource-efficient.

---

### 2. Image Preprocessing

* Images are prepared to ensure compatibility with feature extraction.
* **HOG (Histogram of Oriented Gradients)** is used to extract features from both classes.

---

### 3. Model Training

* A **Linear Support Vector Classifier (Linear SVC)** is used.
* Chosen for its **computational efficiency** and solid performance on binary classification.

---

### 4. Pipeline Construction

The entire process is encapsulated in a **scikit-learn pipeline**:

* **Preprocessing:** Rescaling and formatting the input image.
* **Sliding Windows:** Multiple windows of **varied sizes** scan the image.

  * Step size is proportional to the image size.
  * Inspired by the sliding window + image pyramid technique, but more efficient.
* **Feature Extraction:** HOG descriptors are extracted from each window.
* **Classification:** Linear SVC returns **decision scores** per window.
* **Thresholding:** Filters out windows unlikely to contain a face.
* **Clustering:**

  * **MeanShift** clustering is applied to merge overlapping windows.
  * Reduces multiple detections of the same face to a single bounding box.

---

### 5. Final Output

* Displays all **centered bounding boxes** where the model detects faces.
* Includes **coordinates** of detected faces for potential integration in camera settings optimization.

---
