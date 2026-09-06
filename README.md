# AI-Powered Environmental Issue Detection for San Jose

## 1. Problem

Residents often report environmental issues—such as illegal dumping, blocked storm drains, water contamination concerns, and pipe leaks—through informal messages or images. These reports may contain important information, but the details are often inconsistent, incomplete, or difficult to organize. For example, one resident may write, “There is a strong chemical smell near the creek,” while another may report, “The drain is full of trash after the rain.” Without a consistent format, city staff may need to manually interpret each report before determining the issue type, urgency, location, and appropriate department. This project focuses on improving the first step of the reporting process: transforming unstructured community reports into organized information that can support human review, data analysis, and future routing to city services. The project is designed to support communities affected by environmental hazards while avoiding assumptions about the cause of those hazards or the people living in affected areas.

## 2. AI Capability

The project uses schema-guided prompting and multimodal AI analysis. The initial version of the system asked the AI to extract information using a simple prompt:

> “Extract water issue info.”

This approach often produced free-form text. Although the response might contain useful information, it did not consistently use the same format or field names. This made the output difficult for another system to process automatically.

To improve consistency, we created a predefined output schema. The AI is instructed to return exactly seven fields:

```json
{
  "location": "",
  "issue_type": "",
  "contaminants_observed": [],
  "urgency": "",
  "affected_entities": [],
  "department": "",
  "resident_language": ""
}
```

The schema helps organize the information into predictable, machine-readable records. These records could later be stored in a database, analyzed in Power BI, or reviewed by city staff before any action is taken.

The project also uses image analysis to examine uploaded images of possible environmental issues, such as trash accumulation, blocked drains, standing water, or visible infrastructure damage.

## 3. Workflow

### Input

The current prototype accepts:

* Written environmental issue reports
* Uploaded images
* Reports submitted in different languages
* Information such as location, visible conditions, and possible community impact

### AI processing

The AI:

1. Reads the resident’s written report.
2. Identifies the general issue type.
3. Extracts the reported location.
4. Identifies possible contaminants or visible hazards.
5. Estimates the urgency level.
6. Identifies affected people, infrastructure, or natural resources.
7. Detects the language of the report.
8. Suggests a department or service that may be appropriate for follow-up.
9. Returns the information in a structured JSON format.

For images, the AI provides a description of the visible condition and can suggest a possible issue category, urgency level, and next step.

### Output

A structured report may look like this:

```json
{
  "location": "Oak Street and King Avenue, San Jose",
  "issue_type": "storm drain blockage",
  "contaminants_observed": ["trash"],
  "urgency": "HIGH",
  "affected_entities": ["residents", "street drainage"],
  "department": "Public Works",
  "resident_language": "Spanish"
}
```

The output can support:

* Consistent data entry
* Report categorization
* Manual triage
* Department recommendations
* Future database storage
* Trend analysis and dashboards

The department recommendation is only a preliminary suggestion. It should be verified using official city procedures, and emergency situations should be handled through the appropriate emergency channels.

## 4. Implemented Features

The current prototype demonstrates:

* Text-based environmental issue extraction
* Schema-guided JSON generation
* Standardized issue categories
* Urgency classification
* Location and department extraction
* Language identification
* Image upload and image-based analysis
* Testing across multiple environmental scenarios
* A failure case involving unstructured AI output
* Human oversight for high-risk reports

## 5. Future Features

The following features are proposed for future development and are not currently implemented in this prototype:

* Real-time IoT water sensors
* Live weather and rainfall data
* Predictive contamination modeling
* Automated connection to San Jose 311 systems
* Real-time alerts to city departments
* Interactive environmental risk maps
* Historical infrastructure and maintenance data
* A public-facing mobile application
* A Power BI dashboard for report trends

## 6. Failure Case

The original prompt was:

```text
Extract water issue info.
```

A possible response was:

```text
There's dirty water and trash near a creek on Elm Street. This appears to be a water contamination issue with possible waste pollutants. The situation may require attention due to potential health risks.
```

### Why this response failed

The response contains useful information, but it is not structured consistently. Important fields such as location, issue type, urgency, contaminants, and department are not clearly separated.

If a program expects JSON, this response may cause a parsing error. It would also be difficult to compare this report with other reports because the information is presented as a paragraph.

### Improvement

We introduced a schema-guided prompt that requires the model to return valid JSON with predefined field names. This makes the result easier to validate, store, filter, and analyze.

However, schema-guided prompting does not guarantee that every prediction is correct. The output still requires validation and, when necessary, human review.

![Example of unstructured AI output](https://github.com/user-attachments/assets/17f3f671-c638-4efb-aa39-3ff2fc65f455)

## 7. Oversight and Tradeoffs

AI-generated reports should not be sent directly to city departments without review in every situation.

Reports labeled as HIGH or CRITICAL, reports with low confidence, and reports with missing or unclear locations should be reviewed by a person before escalation. Human review can help identify incorrect classifications, false alarms, and situations where the AI has made assumptions that are not supported by the report or image.

The main tradeoff is between speed and reliability:

* Automated processing can reduce repetitive manual work and organize reports quickly.
* Human review requires additional time and staff resources.
* Strict schemas improve consistency but may not capture every detail in an unusual report.
* Image analysis can help identify visible conditions but cannot confirm contamination or determine whether water is safe.
* Department recommendations can support triage but should not replace official procedures.

## 8. Responsible Use

This prototype is intended to assist with report organization and preliminary triage. It should not:

* Determine whether water is safe to drink
* Diagnose public-health conditions
* Make emergency decisions independently
* Replace city inspections
* Automatically blame a person or community for an environmental issue
* Send high-risk reports to agencies without human review

The original resident report and any uploaded image should be preserved alongside the AI-generated output so that reviewers can compare the source information with the model’s interpretation.

## 9. Evaluation Plan

To evaluate the system, we would create a labeled test set containing environmental reports with expected values for:

* Issue type
* Urgency
* Department
* Language
* Location extraction

The AI output would then be compared with the expected labels. Future evaluation should measure:

* Field-level accuracy
* Issue classification accuracy
* Urgency classification accuracy
* Language detection accuracy
* JSON validity rate
* Human-review rate
* Common error types

The current project demonstrates the AI workflow and structured-output design. A larger labeled dataset is needed before making formal accuracy claims.

## 10. Conclusion

This project demonstrates how AI can transform inconsistent environmental reports into structured records that are easier to review and analyze.

The main contribution is not simply generating an AI response. It is designing a more reliable workflow that includes structured output, failure-case testing, image analysis, human oversight, and responsible-use considerations.

With additional testing, database integration, and a Power BI dashboard, this prototype could be extended into an analytics system for identifying environmental issue trends across San Jose.

## Technologies

* Python
* Google Gemini API
* Google Colab
* JSON
