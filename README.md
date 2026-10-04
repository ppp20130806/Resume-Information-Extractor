# Resume Information Extractor (Resume2Table)

**Course:** PE6201 Emerging AI Technologies
**Student:** Pu Hongyu
**Project Type:** End-of-Course Project - Milestone 2

## 📌 Persona & Problem Statement
- **Primary User:** Mei, an HR Recruiter who processes hundreds of resumes daily.
- **Problem:** Manual data entry from unstructured resumes to internal systems is time-consuming, error-prone, and slows down the hiring process.
- **Solution:** An LLM-powered extraction pipeline that converts unstructured resume text into structured data (Name, Email, Skills, Years of Experience).

## 📥 Input & Output
- **Input:** Plain text resumes (CSV format) containing diverse formatting, multiple languages, and edge cases.
- **Output:** Structured JSON/CSV data with four extracted fields.
- **Architecture Diagram:** 
  ![Architecture](architecture.png)
  *(Flow: Text Input -> Prompt -> OpenRouter LLM -> JSON Parser -> Guardrails Layer -> Final Output)*

## 📊 Metrics Targeted vs. Reached
Based on a synthetic dataset of 25 resumes (containing edge cases like missing emails, soft skills, and fresh graduates):

| Metric | Targeted | Reached |
|---|---|---|
| Name Accuracy | > 85% | **100%** |
| Email Accuracy | > 95% | **100%** |
| Skills Accuracy | > 70% | **100%** (With Guardrails) |
| Years Accuracy | > 80% | **88%** |
| **Overall Accuracy** | > 80% | **88%** |

*Note on Skills: Initial evaluation without guardrails was 88%. By implementing a business-rule guardrail to filter out soft skills (e.g., "communication", "leadership") and normalize formats, Skills Accuracy reached 100%.*

## 💰 Cost Analysis (Build vs. Buy)
- **Build:** Prompt engineering, JSON parsing logic, and Guardrail rules.
- **Buy (Rent):** OpenRouter API (LLM) and Google Colab (compute).
- **Cost per resume:** ~$0.00 (using free tier models like Apodex/Gemma).
- **Human Cost per resume:** ~$0.25 SGD (assuming 30 seconds per resume at $30/hr).
- **Conclusion:** High cost-efficiency and massive ROI for high-volume recruitment.

## 🛡️ Risks & Limitations
- **Silent Failure:** LLMs can confidently hallucinate or format data incorrectly. 
- **Mitigation:** The Guardrails layer validates email formats via regex and filters soft skills. However, **Human-in-the-loop** is required for "Years of Experience" because LLMs struggle to infer "0 years" from "just graduated."
- **Privacy:** Used synthetic data to comply with PDPA and avoid PII leaks.

## 🚀 How to Run
1. Open the `resume_extractor.ipynb` in Google Colab.
2. Upload `ground_truth_25.csv` to the Colab environment.
3. Set your OpenRouter API Key in the notebook.
4. Run the extraction loop to generate `llm_results.csv`.
5. Run the evaluation code block to calculate accuracy and apply Guardrails.
