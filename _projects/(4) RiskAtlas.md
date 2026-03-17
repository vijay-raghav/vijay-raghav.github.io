---
name: RiskAtlas
tools: [AI, Supply Chain Tech, Predictive Analytics, Graph Visualization]
image: ../assets/images/risk-atlas.png
description: A predictive multi-tier Supply Chain Risk Management engine with AI-powered incident triage.
---
# RiskAtlas: AI-Powered Supply Chain Visibility & Impact Analysis

**Live Demo:** [https://riskatlas-prodhacks.lovable.app/](https://riskatlas-prodhacks.lovable.app/)

### Slide Deck
<iframe src="https://pitch.com/embed-link/sguyde" allow="fullscreen; clipboard-write" allowfullscreen="" width="100%" height="500" style="border:0; margin-top: 10px; margin-bottom: 20px;"></iframe>

*RiskAtlas was built at **[ProdHacks '26](https://prodhacks.com/)** under the Intelligence Tools track, which challenged participants to build a functional prototype of a new digital enterprise product or feature.*

Modern supply chains act as complex, multi-tiered networks. Having worked in supply chain transformation, I understand the sheer magnitude and financial cost of this problem firsthand: alerts don't translate into *what* breaks and *why* fast enough. Decisions happen in meetings. Communication is scattered on emails and chats. There is no system of record. When an incident occurs at a Tier-3 supplier, there is no shared view between the **Risk Manager** (who spots issues), the **Production Planner** (who protects the schedule), and **Plant Operations** (who executes actions).

**RiskAtlas** is an interactive product prototype I built to demonstrate what a modern "**Supply Chain Risk Monitoring**" tool looks like. It leverages AI incident analysis to map out multi-tier disruption pathways algorithmically, shifting risk management from reactive to predictive.

### The Product Vision

1. **Information Asymmetry:** Supply Chain Risk teams hear about global events (e.g., port strikes, typhoons) on the news but have no immediate mathematical way to calculate how that news translates to their specific operational risk.
2. **The "Opaque Tier" Problem:** Companies usually know their direct (Tier-1) suppliers, but lack visibility into the deeper sub-tier network where the majority of risks actually originate.
3. **Slow Mitigation:** By the time a disruption reaches the final assembly plant, expensive emergency freight or line stoppages are the only options remaining.

### The Solution: A Predictive AI Risk Monitor
With **RiskAtlas**, supply chain managers input unstructured incident reports into an intelligent ingestion engine which automatically computes the downstream blast radius. The UI is centered around a **Risk Radar Dashboard** tracking global active incidents and a **Network Impact Preview**. It provides a **Shared Context** alignment tool between Risk Managers (who spot the issues), Production Planners (who protect the schedule), and Plant Operations (who execute the mitigations).

*   **AI-Driven Incident Triage:** Instead of manually reading intelligence reports, users paste unstructured text into the `Incidents` portal. A backend AI edge function immediately extracts the incident's category, assigns a 1-5 severity score, calculates algorithmic confidence levels, and identifies all affected entities both geopolitically and conceptually.
*   **The Multi-Tier Impact Graph (`React Flow`):** This is the core visualization engine of the product. Once an incident is triaged, RiskAtlas traverses a complex relationship graph. It visually plots the incident propagating rightward from the event origin -> to Tier-3 suppliers -> to Tier-2 -> Tier-1 -> the affected vehicle/product programs -> and finally the delayed assembly plants. 
    * *Product Note:* Visually mapping this out using interactive, color-coded node graphs (powered by `React Flow`) allows users to instantly comprehend the "blast radius" instead of staring at spreadsheets.
*   **Intelligent Propagation Logic:** The app algorithms do not just guess; they perform geographic radius matching, NLP-based commodity matching, and multi-hop upstream walking to accurately connect an isolated event to concrete organizational dependencies.
*   **Human-in-the-Loop Validation:** Supply chain decisions carry massive financial weight, so algorithmic guardrails are critical. If the AI agent's confidence score for an incident summary falls below 0.65, the system blocks automated mitigation proposals and routes the signal for mandatory human review.

### Go-to-Market & Adoption Strategy
Introducing predictive AI to legacy supply chain operations requires a phased approach to build trust. RiskAtlas is designed around a **"Walk, Run, Fly"** adoption model:
1.  **Walk:** The system acts passively, parsing signals and mapping the graph, but all mitigation actions (e.g., expediting freight) must be manually approved by a human operator.
2.  **Run:** The system is trusted to automatically execute lower-risk, reversible mitigations (like querying alternate suppliers for capacity) while reserving high-impact decisions for human review.
3.  **Fly:** Autonomous execution of defined playbooks based on historical success rates.

### End-to-End AI Architecture

<script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script>
<script>mermaid.initialize({startOnLoad:true});</script>

<div class="mermaid" style="display: flex; justify-content: center; margin-bottom: 2rem;">
graph TD
    Input[Unstructured Intelligence Report]
    LLM{AI Triage Engine}
    Graph[(Supply Chain Knowledge Graph)]
    Mitigation[AI Mitigation Generator]
    UI[Command Center Dashboard]
    Approval[Human-in-the-Loop Validation]

    Input -->|"1. Ingest News/Alert"| LLM
    LLM -->|"2. Extract Entities & Severity"| Graph
    
    Graph -->|"3. Propagate Downstream Impact"| Mitigation
    Graph -->|"4. Visualize Blast Radius"| UI
    
    Mitigation -->|"5. Prescribe Actions"| Approval
    Approval -->|"6. Confirm/Override"| UI

    style LLM fill:#f9d0c4,stroke:#333,stroke-width:2px
    style Mitigation fill:#f9d0c4,stroke:#333,stroke-width:2px
    style Graph fill:#bfe6ff,stroke:#333
    style UI fill:#e1f7d5,stroke:#333
</div>

Rather than simply acting as a database viewer, RiskAtlas is designed around an active AI propagation pipeline that transforms unstructured chaos into actionable strategy:

1. **Unstructured Ingestion & AI Triage:** The flow begins when an unstructured intelligence report (e.g., a news article about a port strike or natural disaster) is ingested. An AI Triage Engine instantly parses the text, extracts the underlying entities (Wait times, Geographic locations, Affected suppliers), and assigns a baseline severity score.
2. **Supply Chain Knowledge Graph Propagation:** Instead of stopping at entity extraction, the system maps those identified entities to the enterprise's multi-tiered `Supply Chain Knowledge Graph`. It mathematically traverses the graph from the origin (e.g., a Tier-3 resin supplier) to calculate the exact downstream impact on Tier-1 suppliers, specific part numbers, and ultimately the delayed vehicle programs and assembly plants.
3. **AI Mitigation Generation:** Once the "blast radius" is computed, the engine proactively generates bespoke mitigation actions (e.g., "Expedite Air Freight," "Qualify Alternate Supplier") complete with cost/time tradeoff analysis.
4. **Human-in-the-Loop Validation:** Supply chain decisions carry massive financial weight. The system operates as a co-pilot, not an autopilot. Every AI-generated finding and prescribed mitigation action requires human validation before being executed through the active Approval dashboard.

### Product Impact & Execution

By heavily focusing on the user experience with tools like the interactive impact map, RiskAtlas serves as a highly compelling proof-of-concept for enterprise software design. 

As a PM, conveying highly dense, interconnected graph data in a way that doesn't overwhelm the user is an immense design challenge. RiskAtlas proves that enterprise resilience tools can be as beautiful, fast, and intuitive as modern consumer software, transforming overwhelming chaos into clear, actionable mitigation paths.

**Defining Success & ROI:**
*   **Time-to-Triage:** The speed at which an unstructured alert is converted into a structured risk profile affecting a specific plant.
*   **Time-to-Approved Plan:** The duration between identifying the risk and having a human operator approve the AI-generated mitigation strategy.
*   **Downtime Avoided:** The ultimate lagging indicator—calculating the financial cost of the line stoppages that were prevented by early mitigation.
