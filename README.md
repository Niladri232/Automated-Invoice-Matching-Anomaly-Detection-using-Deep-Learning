Invoice Intelligence: Multi-Layered Information Extraction & Forensic Fraud Detection

An end-to-end intelligent document processing (IDP) and verification pipeline. This framework transforms noisy, unstructured physical receipts and invoices (using the SROIE 2019 dataset) into pristine structured data, and evaluates it through a forensic anomaly detection engine to flag transaction fraud (e.g., invoice splitting, inflated amounts, and geometric tampering).

📌 Project Overview & Pipeline Architecture
Manual invoice auditing is highly inefficient, error-prone, and vulnerable to sophisticated financial leakage. This project implements a Three-Tiered Deep Learning & Auditing Framework to automate ingestion and security validation.

Layer 1 (Vision): Handles pixel-level cleanup (Otsu's binarization, affine deskewing), super-resolution upscaling, bilateral denoising, and character extraction.

Layer 2 (NLP & Layout): A multi-modal sequence labeler (LayoutLM/BERT) that binds word semantics with 2D spatial coordinates to produce structured BIO (Beginning-Inside-Outside) token blocks.

Layer 3 (Forensics & Anomaly): Aggregates raw tokens into structured tables, executing mathematical validation, entity verification, statistical behavioral drift check, and micro-skew bounding box forensics.

⚡ Core Features

1. Advanced Computer Vision Normalization

Active Deskewing: Dynamic rotation correction calculated using cv2.minAreaRect contours.

Super-Resolution Upscaling: Bicubic $2\times$ interpolation sharpens tiny, blurry thermal paper ink trails.

Bilateral Filtering: Denoises noisy backgrounds (paper creases, camera shadows) while keeping character strokes crisp.

Reading-Order Row Bucketing: Combines split columns into a natural left-to-right human reading grid using a $Y$-axis corridor tolerance threshold.

2. Robust Token-BIO Alignment (Vision-to-NLP Bridge)

Avoids substring matching collisions (e.g. matching TA to TALK) via exact token boundaries.

Preserves bounding box mappings and handles split decimal floats (e.g. aligning 9 . 00 back to 900 total value targets).

Structured output maps directly into deep learning document transformer tokenizers.

3. Smart Forensic Audit Engine

Mathematical Balance Checks: Confirms $\sum \text{Line Items} = \text{Total Amount}$.

Historical Behavioral Profiling: Flags statistical outliers (Z-scores) in transaction value or submission timing based on past vendor baseline histories.

Document Modification Audit: Scans 2D bounding boxes on high-value targets (totals, tax) to catch micro-skews indicative of physical image forgery.
