---
name: Feedback Analyzer
tools: [AI, Serverless, Product Management, Analytics Dashboard]
image: ../assets/images/feedback-analyzer.png
description: An Intelligent Feedback Analysis Engine built for Product Managers.
---
# Product Case Study: Feedback Analyzer - Turning Raw User Input into Actionable Insights

As a Product Manager, parsing through hundreds of scattered user feedback tickets (from Twitter, support emails, and Discord) is an operational nightmare. The **Feedback Analyzer** is a serverless, AI-powered ingestion engine and dashboard that I built to automate this process, allowing PMs to spend less time categorizing issues and more time solving the *right* problems.

### The Core Problem

Through personal PM experience, I realized feedback often gets lost in unmonitored Slack channels, meeting notes, and scattered documents. This validated my core assumption: *speed to triage is far more crucial than the speed to fix*. The goal was separating signal from noise.

1.  **Siloed Data:** Feedback comes from a multitude of disparate channels, making it difficult to get a holistic view of user sentiment.
2.  **Manual Triage is Unscalable:** Reading, categorizing, and scoring the urgency of every piece of feedback manually creates massive bottlenecks.
3.  **Losing the Forest for the Trees:** It's hard to identify recurring themes or semantic similarities (e.g., "cannot log in" vs "auth is broken") using traditional keyword searches.

### The Solution: An Intelligent Ingestion Pipeline

I initially considered "out-of-the-box" AI Search models but realized they were optimized for static documents, not structured data streaming. Therefore, I designed a completely custom serverless architecture using **Cloudflare's Developer Platform** that instantly ingests, processes, and visualizes feedback in real-time.

*   **Smart Orchestration via Workflows:** Instead of keeping users waiting, feedback is ingested via an API that triggers a background `Cloudflare Workflow`. This ensures zero dropped requests, even during massive spikes in feedback volume.
*   **Parallel AI Processing:** Inside the workflow, the text runs through two AI models simultaneously:
    *   **LLaMa-3 (Meta):** Instructed as a strict data classifier to extract a concise summary, categorize the issue (e.g., Bug, Feature Request, Billing), determine sentiment, and assign an Urgency Score (1-5).
    *   **BGE-Base (Embedding Model):** Converts the raw text into a high-dimensional vector to capture its conceptual meaning.
*   **Semantic Search & Analytics:** 
    *   The structured metadata (Summary, Category, Urgency) is stored in **Cloudflare D1** (SQL) to power a real-time analytics dashboard showcasing Top Categories, Critical Issues, and Sentiment splits.
    *   The vector embeddings are stored in **Cloudflare Vectorize**, allowing PMs to perform powerful *semantic searches* (e.g., searching for "login difficulties" will surface tickets that use entirely different wording but mean the same thing).

### Product Impact & Execution

By leveraging a serverless architecture, this tool effectively demonstrates how modern AI can be moved out of the "chatbot" phase and embedded directly into backend data pipelines. 

**Algorithmic Guardrails:**
Automating triage with LLMs introduces risks like hallucination and bias. To mitigate this in a production environment, I implemented two safeguards: **Confidence Thresholds** (if the AI's confidence score is <70%, the item is flagged for mandatory Human Review) and **Strict Enums** (forcing the model to output a predefined category to prevent data pollution).

**Defining Success (Metrics):**
*   **Triage Time Reduction:** The decrease in time between "Feedback Received" and "Ticket Created in Jira / Engineering Tracker."
*   **Deflection Rate:** The percentage of queries answered via the semantic "Search" feature (finding existing solutions) without needing a new human response.
*   **Operational Efficiency:** Automating categorization and assigning an urgency score ensures that Critical (Level 5) issues (like payment failures) are surfaced to the top of the dashboard immediately.
*   **Cost-Effective Scalability:** By utilizing Cloudflare Workers, the platform scales infinitely from zero, meaning you only pay for the exact compute milliseconds used during ingestion.

*Built as part of a product assignment for Cloudflare.*
