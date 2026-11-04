# 🫁 Automated Lung Nodule Detection & Clinical Decision Support System

> **TÜBİTAK Supported Academic Research & Capstone Project**  
> *Faculty of Engineering, Department of Computer Engineering — Inonu University*  
> **Lead Researcher:** Ahmed Dillo  
> **Academic Advisor:** Assoc. Prof. Dr. Ahmet Arif AYDIN  

---

## 📌 Executive Summary

Lung cancer remains one of the leading causes of cancer-related mortality worldwide. Early detection of pulmonary nodules in Computed Tomography (CT) scans significantly improves patient survival rates. However, manual radiological inspection of CT slices is time-consuming and prone to inter-observer variability.

This research presents an **end-to-end Computer Vision & Clinical Decision Support System** that integrates custom DICOM preprocessing, radiological image enhancement, automated YOLO-based nodule detection, and a human-in-the-loop web interface for manual/semi-automated segmentation.

---

## 🏛️ Project Recognition & Funding

* **Supported by:** **TÜBİTAK** (The Scientific and Technological Research Council of Türkiye) — National R&D Support Program.
* **Benchmark Dataset:** Gold-standard **LIDC-IDRI** (Lung Image Database Consortium and Image Database Resource Initiative), comprising 1,012 patient CT scans and ~15,000 radiologist-annotated nodules.
* **Status:** Complete engineering lifecycle (Preprocessing, Model Optimization, Interactive Deployment). Codebase hosted in a private repository for proprietary R&D security.

---

## 🔬 System Architecture & Processing Pipeline

```
[ Raw LIDC-IDRI CT Slices ]
            │
            ▼
[ Multi-Radiologist Mask Fusion & Binary Thresholding ]
            │
            ▼
[ Image Enhancement: Bilateral Filtering + CLAHE ]
            │
            ▼
[ Automated ROI Extraction & Bounding Box Normalization ]
            │
            ▼
[ Data Augmentation Pipeline (15k -> 46k Crop Samples) ]
            │
            ▼
[ YOLO Object Detection Model Training (mAP50 ~ 72%) ]
            │
            ▼
[ Interactive Streamlit Web Interface & Semi-Auto Masking Tool ]
```

---

## 🌟 Key Modules & Visual Demonstration

### 1. Radiological Noise Reduction & Image Enhancement
To improve model focus on pathological parenchymal structures, raw CT slices undergo a dual-stage enhancement pipeline:
* **Edge-Preserving Bilateral Filter:** Eliminates high-frequency CT scan noise without degrading sharp nodule boundaries.
* **Contrast Limited Adaptive Histogram Equalization (CLAHE):** Enhances soft-tissue contrast within the pulmonary region.

*(Place image here: `assets/enhancement_pipeline.png`)*  
![Image Enhancement & Mask Overlay](./assets/enhancement_pipeline.png)

---

### 2. Region of Interest (ROI) Extraction & Data Augmentation
* **Bounding Box Crop:** Extracts targeted nodule sub-regions based on radiologist annotations.
* **Balanced Augmentation:** Applies spatial rotations (90°, 270°), horizontal/vertical flips, and contrast perturbations—expanding the ROI training pool from **15,424** to **46,272** normalized samples to mitigate overfitting.

*(Place image here: `assets/roi_crop_augmentation.png`)*  
![ROI Extraction and Augmentation](./assets/roi_crop_augmentation.png)

---

### 3. Automated YOLO Nodule Detection Interface
A lightweight **Streamlit** dashboard allows clinicians to upload CT slice images for instantaneous inference:
* **Dynamic Model Inference:** Automatically locates pulmonary nodules using fine-tuned YOLO detection weights.
* **Automated Crop Persistence:** Selects the highest-confidence bounding box, crops the ROI, and routes it to downstream segmentation modules.

*(Place image here: `assets/streamlit_yolo_detection.png`)*  
![YOLO Detection Interface](./assets/streamlit_yolo_detection.png)

---

### 4. Human-in-the-Loop Annotation & Masking Interface
To bridge automated deep learning with clinical expert intervention, a custom web-based free-draw segmentation module was designed:
* **Interactive Free-Draw Masking:** Allows radiologists to refine nodule boundaries using adjustable brush strokes.
* **Ground Truth Persistence:** Generates binary pixel-level masks for continuous model fine-tuning and validation.

*(Place image here: `assets/manual_masking_ui.png`)*  
![Interactive Annotation Tool](./assets/manual_masking_ui.png)

---

## 📊 Technical Specifications & Stack

| Component | Technology / Library |
| :--- | :--- |
| **Language** | Python 3.9+ |
| **Deep Learning** | PyTorch, YOLO (Ultralytics) |
| **Image Processing** | OpenCV (`cv2.bilateralFilter`, `CLAHE`), NumPy, SciPy |
| **Web Framework** | Streamlit, Streamlit-Drawable-Canvas |
| **Evaluation Metrics** | mAP@50 (~72%), Precision, Recall, Loss Stability |

---

## 🛡️ Repository Notice & Licensing

> **Note on Source Code Access:**  
> The core algorithmic scripts, pre-trained weights (`.pt`), and proprietary dataset pipeline scripts are maintained in a **Private Repository** to preserve project IP and ongoing research manuscript preparation.  
> 
> *For academic inquiries, collaboration requests, or live system demonstrations, please contact the lead developer.*

---

## ✉️ Contact

**Ahmed Dillo**  
*Computer Engineering B.Sc. (Faculty Valedictorian) | M.Sc. Candidate in Software Engineering*  
* **Email:** ahmeddillo4444@gmail.com  
* **LinkedIn:** [linkedin.com/in/ahmed-dillo](https://www.linkedin.com/in/ahmed-dillo/)  
* **GitHub:** [github.com/Ahmeddillo](https://github.com/Ahmeddillo)
