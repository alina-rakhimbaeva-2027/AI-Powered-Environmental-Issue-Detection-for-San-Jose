## AI-Powered Environmental Issue Detection for San Jose

This project uses artificial intelligence to identify environmental issues in San Jose, such as litter, pollution, damaged infrastructure, and other community concerns. It demonstrates how computer vision and data analysis can support smarter, faster, and more sustainable urban problem-solving.

Open the notebook in Google Colab
https://colab.research.google.com/drive/1h3ky9RWIrerttjD5q8yNm6aZHXRMq6sa?usp=sharing

**Project overview**

Residents may report illegal dumping, blocked storm drains, water-quality concerns, or pipe leaks through informal messages and images. The prototype organizes those inputs into a predictable JSON structure so that a reviewer could categorize reports, assess urgency, and identify a possible city service for follow-up.

The project focuses on report organization and preliminary triage. It does not make official referrals, determine whether water is safe, replace inspections, or connect to live San Jose systems.

**What the notebook demonstrates**

- Schema-guided extraction from written reports
- Seven standardized output fields: `location`, `issue_type`, `contaminants_observed`, `urgency`, `affected_entities`, `department`, and `resident_language`
- JSON parsing and validation, including required fields, allowed urgency values, and list types
- Synthetic test cases covering pipe leaks, creek dumping, cloudy tap water, and a Spanish-language storm-drain report
- Multimodal image analysis for visible environmental conditions
- A failure case showing why free-form output is difficult to parse reliably
- Human oversight, limitations, responsible-use guidance, and an evaluation template

**Workflow**

1. A resident report or image is provided as input.
2. The OpenAI Responses API generates a structured preliminary report or image description.
3. The notebook parses and validates the JSON output where applicable.
4. A person reviews high-urgency, ambiguous, low-confidence, or incomplete reports before escalation.

Example output:

```json
{
  "location": "Elm Street near the storm drain",
  "issue_type": "possible water contamination",
  "contaminants_observed": ["unknown"],
  "urgency": "HIGH",
  "affected_entities": ["creek", "residents"],
  "department": "Environmental Services",
  "resident_language": "English"
}
```

**Run in Google Colab**

1. Open the Colab link above.
2. Add an `OPENAI_API_KEY` secret in Colab under **Secrets**.
3. Run the setup and schema cells first.
4. Run the text test cases.
5. For image analysis, upload a synthetic or public-domain image when prompted.

The notebook defaults to `RUN_LIVE_API = True` and uses `gpt-4.1-mini` through the OpenAI Python client. Add an `OPENAI_API_KEY` Colab secret before running. API usage may incur charges. Never commit API keys, private resident reports, or private images.

**Evaluation status**

The notebook includes an evaluation template, but it does not report formal accuracy. A larger labeled dataset is required to measure JSON validity, issue classification, urgency, department suggestions, language detection, location extraction, human-review rate, and common error types.

**Limitations and responsible use**

Image analysis can describe visible conditions but cannot confirm chemical or biological contamination. Department suggestions are preliminary and must be checked against current official procedures. High-risk reports should receive human review before any escalation. The sample reports in this repository are synthetic.

**Future improvements**

- Add confidence scores and automatic human-review flags
- Expand the labeled multilingual evaluation set
- Store validated reports in a database
- Build a Streamlit interface and Power BI trend dashboard
- Integrate official reporting channels only after validation, privacy review, and authorization

**Technologies**

Python · OpenAI API · Google Colab · JSON
