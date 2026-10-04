# Evaluation & Data Explainer

This document explains the data and evaluation files uploaded in this repository.

## Data Used
- **ground_truth_25.csv**: The synthetic dataset of 25 resumes (containing bilingual text, missing fields, HTML tags, and soft skills) used as the ground truth for extraction evaluation.

## Evaluation Iterations (Why are there 3 files?)
- **evaluation_results.csv (Strict Matching)**: Initial evaluation using exact string matching. Accuracy was **52%**. Error analysis revealed the AI was extracting correctly but formatting inconsistently (e.g., returning `['Python']` instead of `Python;`).
- **evaluation_results_v2.csv (Smart Matching)**: Introduced a normalization layer (removing brackets, standardizing casing, set-based comparison for skills). Accuracy increased to **84%**.
- **evaluation_results_v3.csv (With Guardrails)**: Final evaluation after implementing business-rule Guardrails (regex email validation, filtering out soft skills like "Communication"). Overall accuracy reached **88%**, with Skills at **100%**.

## Key Insight
Years of Experience remained at 88% because the LLM could not infer that "I just graduated" equals "0 years of experience." This proves that pure automation is dangerous, and Human-in-the-loop is required for ambiguous semantic cases.
