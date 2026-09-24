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
93% accuracy on a held-out test set (35 train / 15 test, stratified by phase)
96% accuracy under cross-validation
Validated with a confusion matrix, an ablation study, and a generalization test on an unseen frame
Calibration check: 0.18% coverage measured on a known full-disk frame where ground truth is near zero

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
  50 frames captured with a Vaonis Hestia smart telescope during the April 2024 total eclipse (Smugglers Notch, VT). Two real-world data defects were identified and corrected: an instrument vignette ring (handled with size-based rejection) and a burned-in watermark strip (handled with row masking).

    Output
  A structured measurements spreadsheet (12 columns per frame) plus a coverage-vs-time curve, validated against NASA reference contact times.

    Author
  Matthew Burgos, CSIT 491, Montclair State University. Peer reviewed by classmates as part of the course.
