---
name: Sentinel
tools: [AI Agents, FinTech, Compliance Tech, Full-Stack]
image: ../assets/images/tartan-hacks.png
description: The Autonomous AI Adjudication Agent for Financial Compliance 
---
# Sentinel: The Autonomous AML Adjudication Agent

**Live Demo:** [https://sentinel-pi-steel.vercel.app/](https://sentinel-pi-steel.vercel.app/) *(Note: May be temporarily unavailable due to API limits)*

### Slide Deck
<iframe src="https://pitch.com/embed-link/82jp48" allow="fullscreen; clipboard-write" allowfullscreen="" width="100%" height="500" style="border:0; margin-top: 10px; margin-bottom: 20px;"></iframe>

*Built At Tartan Hacks 2026. Sentinel is an AI-powered "Compliance Co-Pilot" that automates the adverse media screening process for financial institutions.*

### The Problem It Solves

- **The Efficiency Crisis**: Financial institutions spend billions annually on compliance, yet **95-99% of transaction alerts are "False Positives."** Analysts waste hours manually Googling names (e.g., "John Smith") to confirm that their 24-year-old student client isn't the 50-year-old money launderer in the news.
- **The Risk of Hallucination**: Standard GenAI chat tools often hallucinate non-existent news or make flawed identity guesses, creating massive regulatory liabilities.
- **Operational Burnout**: The sheer volume of manual verification leads to "alert fatigue," causing analysts to miss actual financial crimes.

### The Solution: A Deterministic Reasoning Engine

Unlike basic LLM wrappers, **Sentinel** acts as an autonomous Adjudication Engine. It ingests customer profiles from Capital One’s Nessie API, scans the live web for negative news using **Model Context Protocol (MCP)** tools, and autonomously adjudicates whether the subject in the news is actually the bank’s client using strict negative constraint logic.

### Technical Agentic Architecture

<script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script>
<script>mermaid.initialize({startOnLoad:true});</script>

<div class="mermaid" style="display: flex; justify-content: center; margin-bottom: 2rem;">
graph TD
    UI[Next.js Workbench UI]
    API[FastAPI Gateway]
    Engine{Dedalus Agent Runner}
    CapitalOne[(Capital One Nessie API)]
    Exa[Exa Search MCP]
    LLM[Anthropic LLM]
    SSE[SSE Handler]

    UI -- "1. Start Adjudication" --> API
    API -- "2. Initiate Workflow" --> Engine
    
    Engine <-->|"3. Retrieve Client Profile"| CapitalOne
    Engine <-->|"4. Scrape Live Web"| Exa
    Engine <-->|"5. Apply Constraint Logic"| LLM
    
    Engine -- "6. Stream Monologue" --> SSE
    SSE -- "7. Real-Time Updates" --> UI
    Engine -- "8. Structured JSON Verdict & SAR" --> UI

    style Engine fill:#f9d0c4,stroke:#333,stroke-width:2px
    style CapitalOne fill:#bfe6ff,stroke:#333
    style Exa fill:#bfe6ff,stroke:#333
    style LLM fill:#bfe6ff,stroke:#333
    style UI fill:#e1f7d5,stroke:#333
    style API fill:#e1f7d5,stroke:#333
</div>

The application is built around a true agentic workflow where various modular systems communicate to achieve an autonomous adjudication vertex. The core intelligence is driven by a **single, multi-phase agent** orchestrated by the Dedalus SDK, rather than a complex multi-agent system.

#### The 3-Phase Single-Agent Workflow
By examining the `SYSTEM_PROMPT` running within the FastAPI backend, we designed the agent to transition sequentially through three distinct personas within a single API call:

1.  **Phase 1: The Researcher (High Recall):** The agent begins by using the **Capital One Customer Information API** (Nessie) to retrieve the client's detailed profile (Age, Location, Account History). It then calls the **Exa Web Search MCP** to query the live internet for adverse media. Crucially, the prompt constrains the search here to *only* use the client's name and risk keywords (avoiding overly specific queries that might drop real news).
2.  **Phase 2: The Analyst (The Filter):** Armed with full article contents scraped by Exa, the agent shifts from recalling data to filtering it. It applies the "Negative Constraint Logic": it assumes the subject in the news is a *different person* until proven otherwise. If it detects a variance—such as a 5-year age gap or a location mismatch between the Nessie profile and the news article—it aggressively throws the result out. It also enforces a "Zero-Result Guardrail," forcing a manual review if no data is found, preventing the agent from falsely clearing a user based on internal model hallucination.
3.  **Phase 3: The Judge (The Verdict):** Finally, the agent evaluates the remaining filtered data against a strict scoring rubric to arrive at a definitive JSON Risk Verdict (Escalate vs. Dismiss), automatically drafting a highly-structured Suspicious Activity Report (SAR) with required URL citations.

#### Why a Single-Agent Architecture?
We deliberately chose a Single-Agent, Multi-Phase approach over a Multi-Agent system (e.g., separate LLMs acting as Researcher, Analyst, and Judge) for three core reasons:

- **Latency:** In compliance adjudication, speed is critical. Passing context back and forth between multiple separate agents introduces massive latency overhead via repeated network calls. Streaming the entire reasoning loop from a single advanced model (Claude Opus) drastically reduces time-to-verdict.
- **Context Retention:** A single agent maintains a flawless native context window. The "Judge" inherently knows exactly *why* the "Researcher" formulated its specific Exa search query, eliminating the need to summarize and compress state between agent handoffs.
- **Deterministic Control:** By rigidly structuring a single system prompt into distinct sequential phases bound by strict rules (like the Zero-Result Guardrail), we achieve the predictability and transparency required by financial regulators, avoiding the unpredictable conversational loops that multi-agent systems often fall into. We originally considered a complex multi-agent system, but it proved too unpredictable and introduced too much latency. Defaulting to a single-agent, multi-phase prompt was a deliberate choice to maintain tight, deterministic control.

#### Real-Time Streaming (SSE) to the UI
As this 3-Phase engine executes, it streams its "inner monologue" (tool calls, search results, and reasoning) through a Server-Sent Events (SSE) Handler back to the **Next.js Workbench UI**. This transparency allows the human analyst to see exactly *how* the AI is reaching its conclusion in real time, ultimately delivering a ready-to-file SAR framework updating the React State.
