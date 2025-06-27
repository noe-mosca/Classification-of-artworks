🖼️ Unsupervised Classification of Artworks by Style

This repository presents a project developed as part of the IMA206 course at Télécom Paris, aiming to cluster digital paintings by artistic style using unsupervised learning techniques, without relying on labeled data. The project explores the combination of handcrafted and deep visual descriptors to build a high-dimensional representation space, which is then reduced and structured using clustering algorithms.

📌 Project Overview

The goal of the project is to automatically group artworks (paintings) by visual and semantic similarity, in an unsupervised setting. The only metadata available was the artist’s birth date. Our pipeline includes:
	•	Visual feature extraction: color, texture, semantic themes.
	•	Deep representations: CLIP and ResNet50 embeddings.
	•	Dimensionality reduction using PCA.
	•	Clustering via K-means and probabilistic assignment (softmax).
	•	Stylistic interpretation of clusters based on artist prevalence.

⸻

🧠 Methodology

1. Feature Extraction
	•	Color Descriptors:
	•	Mean and standard deviation of HSV components.
	•	Dominant colors extracted with K-means on pixel-level HSV data.
	•	Texture Descriptors:
	•	Features from Gray-Level Co-occurrence Matrices (GLCM): contrast, energy, homogeneity, etc.
	•	Thematic Descriptors:
	•	Embeddings from the CLIP model (OpenAI) to capture semantic content (objects, scenes, atmosphere).

2. Deep Representations
	•	ResNet50 Embeddings:
	•	2048-dimensional features extracted from the final convolutional layers of ResNet50.
	•	CLIP Embeddings:
	•	512-dimensional vectors capturing image-language correspondence.
	•	Fusion:
	•	All features were concatenated, normalized, and combined into a single representation per painting.

3. Dimensionality Reduction
	•	Principal Component Analysis (PCA):
	•	Reduced vectors to 1000 dimensions, preserving over 90% of the total variance.

4. Clustering
	•	K-means Clustering:
	•	Applied in PCA space with 𝑘 = 50 clusters.
	•	Initializations with K-means++ and multiple seeds to ensure stability.
	•	Probabilistic Assignment:
	•	Softmax over distances to centroids with optional penalization terms to account for cluster dispersion.

5. Evaluation
	•	Clusters were interpreted via majority artists per group and cross-referenced with known styles (from WikiArt).
	•	Subjective and visual analysis revealed:
	•	~26 clusters clearly aligned with identifiable styles.
	•	~13 clusters partially coherent.
	•	~11 clusters less interpretable or heterogeneous.

⸻

📊 Results
	•	Styles such as Impressionism, Rococo, or Cubism were well-represented.
	•	Complex styles (e.g., Post-Impressionism) showed more confusion due to their inherent diversity.
	•	The soft assignment approach helped manage ambiguous artworks and smoothen boundaries between close styles.
