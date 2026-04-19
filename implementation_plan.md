# Dynamic LLM-Powered Research Synthesis

Transition the current template-based literature review drafting to a truly dynamic, AI-driven process using the **Gemini 1.5 Flash API** (Free Tier). This will ensure the review structure and content are uniquely tailored to the research theme and the specific findings of the collected articles.

## User Review Required

> [!IMPORTANT]
> **Gemini API Key Needed**: To enable this feature, you will need a free API key from [Google AI Studio (aistudio.google.com)](https://aistudio.google.com/). You will need to add this key to your `agent_config.json` file.
> 
> **Rate Limits**: The free tier of Gemini has rate limits. The system will be designed to handle these gracefully, but the first run might take a minute as it synthesizes the large volume of data.

## Proposed Changes

### Environment & Configuration

#### [MODIFY] [requirements.txt](file:///c:/Users/bilel/OneDrive/Desktop/Autonomous_Research_Agent/requirements.txt)
- Add `google-generativeai` to the dependencies.

#### [MODIFY] [agent_config.json](file:///c:/Users/bilel/OneDrive/Desktop/Autonomous_Research_Agent/agent_config.json)
- [NEW] Add `"gemini_api_key": "YOUR_KEY_HERE"` field.
- [NEW] Add `"model_name": "gemini-1.5-flash"` field.

---

### Drafting Logic

#### [MODIFY] [review_drafter.py](file:///c:/Users/bilel/OneDrive/Desktop/Autonomous_Research_Agent/core/review_drafter.py)
- **Remove Hardcoded Templates**: Delete the `pillars` and hardcoded paragraphs.
- **Gemini Integration**: Implement a client to interact with `google-generativeai`.
- **Dynamic Structural Planning**: 
    1. Send research theme + article titles/abstracts to Gemini.
    2. Ask Gemini to propose a thematic outline (sections and subsections) that best organizes the literature.
- **High-Fidelity Drafting**:
    1. For each section in the outline, prompt Gemini to write a high-quality academic synthesis.
    2. Ensure accurate citations using `\citep{idX}` format.
    3. Enforce the user's word count requirements (e.g., 3000 words).
- **LaTeX Sanitization**: Implement a function to ensure LLM-generated text doesn't break LaTeX compilation (escaping special characters like `%`, `$`, `&`).

---

### Orchestration

#### [MODIFY] [master_agent.py](file:///c:/Users/bilel/OneDrive/Desktop/Autonomous_Research_Agent/master_agent.py)
- Ensure it checks for the Gemini API key before starting the drafting step.

## Open Questions

1. **Language**: Should the synthesis be in **French** (matching your theme description) or **English** (standard for these bibliometric outputs)? Gemini can do both fluently.
2. **Detail Level**: Should we include the full abstracts in the prompt for the 15 top articles, or just titles and snippets? Full abstracts provide better synthesis but use more "input tokens" (though well within Gemini's 1M limit).

## Verification Plan

### Automated Tests
- Run `python core/review_drafter.py` independently to verify Gemini connectivity and LaTeX generation.
- Execute `python master_agent.py` to test the full pipeline.

### Manual Verification
- Inspect `main.pdf` to ensure the structure is thematic and the citations are correctly integrated.
- Verify that the word count matches the configuration targets (~3000 words).
