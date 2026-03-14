# Retinal Cyst Segmentation in OCT Images

### Classical Image Processing Approach (Non-CNN)

This project implements a **fully successful classical image segmentation pipeline** for detecting retinal cysts in **Optical Coherence Tomography (OCT) scans**. The system was developed as part of the **CSC8628 Image Processing assignment at Newcastle University**, where the objective was to design a **pixel-level cyst segmentation algorithm without using convolutional neural networks (CNNs)**. 

The final solution successfully segments retinal cyst regions using a combination of:

* Image preprocessing
* K-Means clustering segmentation
* Morphological refinement
* Watershed boundary refinement

The project achieved **strong segmentation performance**, demonstrating that **classical computer vision techniques can effectively solve medical image segmentation problems without deep learning**.

---

# Project Objective

Retinal cysts are **fluid-filled lesions** that appear in OCT scans and are commonly associated with vision-threatening diseases such as:

* Diabetic Macular Oedema (DME)
* Age-related Macular Degeneration (AMD)

Detecting these cysts manually is **time-consuming and requires clinical expertise**. The goal of this project was therefore to develop an **automatic segmentation algorithm** that can identify cyst regions directly from OCT images. 

The system was required to:

* Perform **pixel-level cyst segmentation**
* Use **classical image processing techniques only**
* Evaluate performance using **quantitative metrics**
* Present results using **visualisations, graphs, and segmentation outputs**

All assignment requirements were **successfully completed**.

---

# Key Features

* Fully automated **retinal cyst segmentation pipeline**
* Designed **without deep learning models**
* Uses **unsupervised clustering (K-Means)**
* Includes **noise reduction and contrast enhancement**
* Implements **multiple segmentation methods for comparison**
* Evaluated using **Dice Score, IoU, Precision, and Recall**
* Generates **visual and quantitative performance analysis**

---

# Methodology

The pipeline consists of **three main stages**.

## 1. Preprocessing

OCT images typically contain **speckle noise and uneven contrast**, which can reduce segmentation quality. Several preprocessing steps were applied to improve image quality.

### Image Normalisation

All images were normalised to an intensity range of **0–255**.

### Median Filtering

A **5×5 median filter** was used to remove speckle noise while preserving cyst boundaries.

### CLAHE (Contrast Limited Adaptive Histogram Equalization)

Improves local contrast and highlights darker cyst regions.

### Gaussian Smoothing

A **5×5 Gaussian blur** was applied to reduce minor intensity variations.

These steps improved the visibility of cyst structures before segmentation. 

---

# Segmentation Algorithms

Three classical segmentation methods were implemented and compared.

## Otsu Thresholding

Otsu’s method performs segmentation using an automatically selected global threshold.

Advantages:

* Simple
* Computationally fast

Limitations:

* Struggles with intensity variation
* May merge multiple cyst regions

---

## K-Means Clustering (Primary Algorithm)

The main segmentation method used in this project was **K-Means clustering**, an unsupervised algorithm that groups pixels based on intensity similarity.

Configuration used:

```
k = 2
Cluster 1 → Cyst regions (darker pixels)
Cluster 2 → Background retinal tissue
```

K-Means proved effective because cysts typically appear **darker than surrounding retinal tissue** in OCT scans.

Advantages:

* Handles brightness variation better than thresholding
* Requires **no labelled training data**
* Computationally efficient

This algorithm produced the **most balanced performance across the dataset**. 

---

## Watershed Segmentation

The watershed algorithm was used as an **optional refinement stage** to improve cyst boundaries.

Advantages:

* Separates touching cyst regions
* Produces more precise segmentation edges

Limitation:

* Higher computational cost

---

# Post-Processing

To improve segmentation quality, morphological operations were applied to remove noise and refine cyst masks.

Operations included:

* Removal of isolated pixels
* Morphological filtering
* Boundary smoothing

These steps significantly reduced **false positive detections**.

---

# Implementation

The system was implemented in **Python 3.10** using open-source libraries.

### Libraries Used

* **OpenCV** – image preprocessing and filtering
* **NumPy** – numerical operations
* **scikit-image** – watershed and morphological processing
* **pandas** – dataset evaluation
* **Matplotlib** – visualisation
* **Seaborn** – statistical plotting

---

# Evaluation Metrics

Segmentation performance was evaluated using four standard metrics.

### Dice Coefficient

Measures the overlap between predicted cyst regions and ground-truth masks.

### Intersection over Union (IoU)

Ratio of the intersection area to the union area of predicted and ground truth masks.

### Precision

Measures the proportion of detected cyst pixels that are correct.

### Recall

Measures the proportion of true cyst pixels successfully detected.

These metrics provide a comprehensive evaluation of segmentation accuracy. 

---

# Results

The developed system successfully segmented cyst regions across the provided dataset.

Key findings:

| Method             | Performance                                |
| ------------------ | ------------------------------------------ |
| Otsu Thresholding  | Fast but less accurate                     |
| K-Means Clustering | Best balance of speed and accuracy         |
| Watershed          | Most precise but computationally expensive |

Final performance achieved:

* **Dice Score:** 0.74
* **IoU:** 0.59

K-Means clustering demonstrated the most effective trade-off between **accuracy, robustness, and computational efficiency**. 

Overall, the system successfully completed the assignment objective of **automatic retinal cyst segmentation using classical image processing methods**.

---

# Example Outputs

The notebook generates several outputs including:

* Preprocessing visualisations
* Filter comparisons
* Segmentation results for each method
* Cyst masks for all OCT images
* IoU and Dice score graphs
* Segmentation performance distributions

---

# Repository Structure

```
retinal-cyst-segmentation
│
├── dataset/
│   ├── OCT_images
│   └── ground_truth_masks
│
├── notebooks/
│   └── cyst_segmentation.ipynb
│
├── results/
│   ├── segmentation_outputs
│   ├── evaluation_plots
│   └── sample_results
│
├── requirements.txt
└── README.md
```

---

# How to Run

### 1 Clone the repository

```bash
git clone https://github.com/yourusername/retinal-cyst-segmentation.git
cd retinal-cyst-segmentation
```

### 2 Install dependencies

```bash
pip install -r requirements.txt
```

### 3 Launch the notebook

```bash
jupyter notebook
```

Open the notebook and run all cells to reproduce the segmentation pipeline.

---

# Future Improvements

Although the system achieved strong results, several improvements could be explored:

* Spatially constrained K-Means clustering
* Texture-based segmentation features
* Hybrid classical + deep learning models
* 3D OCT volume segmentation
* Comparison with architectures such as U-Net

---

# Conclusion

This project successfully demonstrates that **classical image processing techniques can accurately segment retinal cysts in OCT images without the use of deep learning models**.

Through careful preprocessing, clustering-based segmentation, and morphological refinement, the proposed pipeline achieved reliable segmentation results and satisfied all assignment objectives.

The work highlights the continued relevance of **traditional computer vision algorithms in medical image analysis**, particularly in environments where deep learning resources may not be available.

---

# References

1. IEEE – Retinal cyst detection methods
2. [https://ieeexplore.ieee.org/document/9635099](https://ieeexplore.ieee.org/document/9635099)
3. [https://pmc.ncbi.nlm.nih.gov/articles/PMC6858411/](https://pmc.ncbi.nlm.nih.gov/articles/PMC6858411/)


