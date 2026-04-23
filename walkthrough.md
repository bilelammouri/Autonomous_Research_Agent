# Dynamically Generated Research Synthesis (Gemini 1.5 Flash)

Monsieur le Professeur, your system is now upgraded to include **real-time, dynamic synthesis** of research articles using the **Gemini 1.5 Flash API**. This transition completely replaces hardcoded templates with an intelligent process that adapts to your theme and the articles you collect.

## Key Upgrades

### 1. Thematic Planning
The `review_drafter.py` now starts by sending the theme and the list of collected articles to the LLM. Instead of using predefined rubrics, the LLM proposes a **thematic structure** (outline) that fits the current research landscape.

### 2. Deep Synthesis (Q1 Standard)
For each section in the proposed outline, the system:
- Sends the **full abstracts** of the top 15 articles to Gemini.
- Requests a **high-density academic synthesis** in English.
- Target: A style and depth suitable for a **Q1 Journal**.
- Automatically handles **citations** using `\citep{idX}` based on the source data.

### 3. LaTeX Integrity
A new `latex_escape` layer has been added to sanitize the output from the LLM, ensuring that special characters (like `%`, `&`, or `_`) often used by researchers don't break the PDF compilation.

---

## How to Run Your New Pipeline

### Step 1: Add your Gemini API Key
Open your `agent_config.json` and replace `"YOUR_GEMINI_API_KEY_HERE"` with your actual key from [Google AI Studio](https://aistudio.google.com/).

```json
{
    ...
    "gemini_api_key": "YOUR_ACTUAL_KEY_HERE",
    "model_name": "gemini-1.5-flash"
}
```

### Step 2: Execute the Orchestrator
Launch the mission as usual:
```powershell
python master_agent.py
```

### Step 3: Inspect the Result
The finished product will be in **`main.pdf`**. It will now feature:
- A unique, theme-specific structure.
- English academic synthesis of approximately 3000 words.
- Professional LaTeX formatting.

---

## Technical Log
- **Model used**: Gemini 1.5 Flash (chosen for its 1M context window and free tier).
- **Library**: `google-generativeai` (installed and configured).
- **Orchestration**: `master_agent.py` now verifies the API key before starting.

The system is now fully "Dynamic" as you requested.
