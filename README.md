# Extracting GD&T from Engineering Drawings using Machine Learning

This repository contains the code and findings for a project on automatically extracting dimensional values from 2D engineering drawings using a machine learning pipeline.

This project was submitted in partial fulfillment of the requirements for **ME F366: Laboratory Project** at **BITS Pilani, Hyderabad Campus**.

* **Author:** Savitra Vardhan Roy
* **Supervisor:** Dr. Kurra Suresh
* **Date:** October 2025

---

## 🚀 Project Overview

Interpreting 2D engineering drawings is a critical step in automating modern manufacturing processes. This project establishes a foundational ML system to analyze these drawings, focusing on the specific task of extracting dimensional values.

Our approach is a **two-step pipeline**:

1.  **Dimension Detection:** A **YOLOv8** object detection model is trained to identify and draw bounding boxes around all dimension text on a drawing.
2.  **Value Extraction:** The content within each bounding box is then processed by an **Optical Character Recognition (OCR)** model to extract the final numerical value.

---

## 1. Dataset

* A custom dataset of **~140 images** was created by manually scraping 2D engineering drawings from sources like **GrabCAD, Pinterest, and online textbook PDFs**.
* All images were resized to a uniform $600 \times 400$ pixels.
* Annotations were performed using **Roboflow**, with an initial single class: `dimensions`.

---

## 2. Step 1: Dimension Detection (YOLOv8)

We evaluated several object detection architectures (including R-CNN and DETR) but selected **YOLOv8** for its high-speed inference, fast convergence, and effectiveness on smaller datasets.

### Training & Results

The final model is a **YOLOv8 medium-sized** variant (25.8M parameters) trained on 132 images for 300 epochs.

**Key Performance Metrics:**
* **mAP50:** 0.988
* **Precision:** 0.975
* **Recall:** 0.99

---

## 3. Step 2: Value Extraction (OCR)

We compared two distinct methods for extracting the text from the bounding boxes predicted by YOLOv8:

### Experiment 1: Pytesseract

* **What it is:** A popular, open-source OCR engine.
* **Result:** **Performed poorly.** It struggled to interpret text correctly, even on very clear, non-oriented images.

### Experiment 2: Google Vision Language Model (VLM)

* **What it is:** A generative multimodal model that can learn from both images and text.
* **Result:** **Performed significantly better**. It accurately interpreted complex and angled measurements (e.g., 'R10' as '10' and '4xR5' as '5') with high precision using a targeted prompt.

---

## 🛠️ How to Use

### Installation

This project relies on several Python libraries. You can install them using pip:

```bash
pip install ultralytics pytesseract opencv-python pandas requests pillow
