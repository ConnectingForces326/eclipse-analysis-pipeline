    Solar Eclipse Analysis Pipeline

A Python computer vision pipeline that measures solar eclipse coverage, sunspot counts, and eclipse phase from consumer smart-telescope images, built for CSIT 491 at Montclair State University.

    What it does
  Given a set of telescope frames from the April 2024 total eclipse, the pipeline:
Segments the solar disk and moon silhouette from each frame
Fits the solar limb using RANSAC circle fitting
Computes eclipse coverage percentage and detects sunspots via connected-component analysis
Classifies eclipse phase (partial, near-total, total) using trained classifiers
Flags low-confidence measurements based on circle-fit error

    Results
- 97% accuracy on a held-out test set, 94% under 5-fold cross-validation (KNN)
- With the coverage feature removed, still 97% held-out / 91% cross-validated, confirming the other measured features carry real signal
- Validated with a confusion matrix and a coverage-ablation study; see eclipse_classifier_training.ipynb for the full training and evaluation code

    Approach
  Deliberately classical and deterministic, no generative AI, no neural networks. Every output is traceable by hand:

Grayscale conversion, Gaussian blur, Otsu thresholding
Morphological cleanup and connected-component analysis
RANSAC circle fitting for the solar limb
Gaussian background subtraction
k-nearest-neighbors (k=5), logistic regression, and decision tree classifiers

    Tech stack
  Python, OpenCV, NumPy, pandas, scikit-learn, openpyxl

    Data
120 frames captured with a Vaonis Hestia smart telescope during the April 2024 total eclipse (Smugglers Notch, VT).

    Output
  A structured measurements spreadsheet (12 columns per frame) plus a coverage-vs-time curve, validated against NASA reference contact times.

    Author
  Matthew Burgos, CSIT 491, Montclair State University. Peer reviewed by classmates as part of the course.
