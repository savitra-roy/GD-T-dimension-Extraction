# Extracting GD&T from Engineering Drawings using Machine Learning

[cite_start]This repository contains the code and findings for a project on automatically extracting dimensional values from 2D engineering drawings using a machine learning pipeline[cite: 3].

[cite_start]This project was submitted in partial fulfillment of the requirements for **ME F366: Laboratory Project** at **BITS Pilani, Hyderabad Campus**[cite: 9, 10].

* [cite_start]**Author:** Savitra Vardhan Roy [cite: 5]
* [cite_start]**Supervisor:** Dr. Kurra Suresh [cite: 8]
* [cite_start]**Date:** October 2025 [cite: 11]

---

## 🚀 Project Overview

[cite_start]Interpreting 2D engineering drawings is a critical step in automating modern manufacturing processes[cite: 33]. [cite_start]This project establishes a foundational ML system to analyze these drawings, focusing on the specific task of extracting dimensional values[cite: 34].

Our approach is a **two-step pipeline**:
1.  [cite_start]**Dimension Detection:** A **YOLOv8** object detection model is trained to identify and draw bounding boxes around all dimension text on a drawing[cite: 35].
2.  [cite_start]**Value Extraction:** The content within each bounding box is then processed by an **Optical Character Recognition (OCR)** model to extract the final numerical value[cite: 37, 38].

---

## 1. Dataset

* [cite_start]A custom dataset of **~140 images** was created by manually scraping 2D engineering drawings from sources like **GrabCAD, Pinterest, and online textbook PDFs**[cite: 50, 54].
* [cite_start]All images were resized to a uniform $600 \times 400$ pixels[cite: 51].
* [cite_start]Annotations were performed using **Roboflow**, with an initial single class: `dimensions`[cite: 53, 55].

---

## 2. Step 1: Dimension Detection (YOLOv8)

[cite_start]We evaluated several object detection architectures (including R-CNN and DETR) but selected **YOLOv8** for its high-speed inference, fast convergence, and effectiveness on smaller datasets[cite: 96, 165].

### Training & Results
[cite_start]The final model is a **YOLOv8 medium-sized** variant (25.8M parameters) trained on 132 images for 300 epochs[cite: 318, 319].

**Key Performance Metrics:**
* [cite_start]**mAP50:** 0.988 [cite: 36, 322]
* [cite_start]**Precision:** 0.975 [cite: 36, 322]
* [cite_start]**Recall:** 0.99 [cite: 322]

---

## 3. Step 2: Value Extraction (OCR)

We compared two distinct methods for extracting the text from the bounding boxes predicted by YOLOv8:

### Experiment 1: Pytesseract
* [cite_start]**What it is:** A popular, open-source OCR engine[cite: 510].
* [cite_start]**Result:** **Performed poorly.** It struggled to interpret text correctly, even on very clear, non-oriented images[cite: 39, 542].

### Experiment 2: Google Vision Language Model (VLM)
* [cite_start]**What it is:** A generative multimodal model that can learn from both images and text[cite: 513].
* [cite_start]**Result:** **Performed significantly better**[cite: 39]. [cite_start]It accurately interpreted complex and angled measurements (e.g., 'R10' as '10' and '4xR5' as '5') with high precision using a targeted prompt[cite: 40, 552, 582].

---

## 🔮 Future Work

This project serves as a strong foundation for a more comprehensive GD&T extraction tool. Future development will focus on:

* [cite_start]**Expanding Scope:** Enhancing the system to interpret more complex **Geometric Dimensioning and Tolerancing (GD&T)** details, such as **datums** and **Feature Control Frames**[cite: 42, 589].
* [cite_start]**Model Enhancement:** Either **fine-tuning a Vision Language Model (VLM) locally** [cite: 584] [cite_start]or compiling a much larger, comprehensive dataset for public research[cite: 606].

---

## 🛠️ How to Use

*(You can add your installation and usage instructions here)*

### Installation

```bash
# Example:
git clone [https://github.com/](https://github.com/)[your-username]/[your-repo-name].git
cd [your-repo-name]
pip install -r requirements.txt
