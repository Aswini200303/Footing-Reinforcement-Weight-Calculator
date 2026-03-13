# 🏗️ Footing Reinforcement Weight Calculator
> **Automated Rebar Weight Extraction from Engineering Plan & Schedule PDFs**

This tool calculates total rebar weight for construction projects. It extracts footing marks from structural plans and cross-references them with reinforcement schedules to generate weight reports.

---

## 🚀 Quick Start

1.  **Setup Secrets:** Add the `GEMINI_API_KEY` to your Google Colab "Secrets".
2.  **Launch:** Click the "Open in Colab" badge at the top of the notebook.
3.  **Run All:** Press `Ctrl + F9` to execute all cells.
4.  **Upload:** When prompted, upload your **Plan PDF** and **Footing Schedule PDF**.
5.  **Download Results:** Retrieve your calculated `footing_counts.csv` and `rebar_weight_results.csv` from the file sidebar.

---

## 🛠️ Key Features

*   **AI-Powered Extraction:** Uses Google Gemini to interpret PDF tables and structural notations.
*   **Hybrid Parsing:** Automatically falls back to `pdfplumber` if the API is unavailable.
*   **Dimension Conversion:** Converts feet-inch notations (e.g., 5'-6") to decimal feet automatically.
*   **Standardized Weights:** Includes built-in unit weight mapping for #3 through #18 rebar sizes.

---

## 📋 Assumptions & Logic

To ensure accuracy, the calculator operates on the following engineering assumptions:

*   **Rebar Orientation:** Assumes "EACH WAY, UNO". Calculations include bars for both length and width directions.
*   **Standard Multiplier:** Uses a default multiplier of **4** (Top & Bottom, Each Way) unless specific quantities are parsed.
*   **Rebar Pattern:** Matches schedule patterns like `(Qty) #BarSize` (e.g., `(6) #5`).
*   **Missing Marks:** If a footing mark appears on a plan but is missing from the schedule, it is flagged with a warning and assigned zero weight to prevent calculation errors.

---

## ⚠️ Limitations

*   **Complex Designs:** Does not support hooks, stirrups, or specialized bends.
*   **Scanned Documents:** Best performance is achieved with text-based PDFs. OCR for handwritten or low-quality scans depends on Gemini's vision capabilities.
*   **Layout Sensitivity:** Non-standard or handwritten schedules may require manual verification.

---

## 📦 Tech Stack

![Python](https://img.shields.io)
![Google Gemini](https://img.shields.io)
![Pandas](https://img.shields.io)

---
