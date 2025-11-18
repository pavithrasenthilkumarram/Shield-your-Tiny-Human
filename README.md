# Shield-your-Tiny-Human

A multi-agent AI system for the detection of online risks for children in chats, comments, and other social spaces with the intention of helping families stay safe by precaution-as technology is growing faster day by day.

Technology today is sprinting at a pace that feels almost unreal. Every morning, something new drops — smarter AI, faster algorithms, hyper-personalized feeds, immersive digital worlds. Kids and teens are stepping into this rapidly evolving space long before most adults ever get a chance to understand it. And while this growth is exciting, it creates a very real imbalance: tech evolves daily, but safeguards don’t.
**That gap is exactly where the “Shield-your-Tiny-Human” lives.**

This project explores how AI can act as a gentle but firm shield for kids and teens across digital platforms — chats, gaming lobbies, DMs, comment sections, and social spaces — detecting threats, inappropriate content, manipulation, grooming patterns, toxic language, cyberbullying, and hidden online risks.

Here is the core philosophy behind the project:

>**Technology will always grow — faster than we expect, faster than we can control. But our responsibility grows with it. If we care enough to build systems that think about child safety, fairness, and balance at every step, then innovation and protection can move forward together. Tech doesn’t have to leave humanity behind — we can choose to build tools that hold both progress and ethics in the same hand.**

<img width="1024" height="1000" alt="ChatGPT Image Jun 27, 2116, 03_56_49 PM" src="https://github.com/user-attachments/assets/f12eac5d-c02f-4537-8bba-2d8579575c5c" />



## Problem Statement

Traditional parental controls:

- often block everything or nothing,
- don’t analyze context,
- and don’t reflect the speed of modern digital communication.

Kids from age 7 to 17 encounter digital environments that were never built with them in mind. And parents? They’re trying to supervise worlds they’ve never lived in.
So the question becomes honest and urgent:

_**Can AI be part of the solution instead of part of the chaos?**_

Families need a smarter, more balanced way to keep children safe online — **without isolating them from technology.**

## Solution

Most safety tools either:

- Over-police (blocking everything),  or
- Under-protect (missing real threats).

This agent is designed to sit in the middle path:
`Balanced Safety = Safety + Autonomy + Privacy`

- It respects kids’ independence.
- It alerts only when something is genuinely concerning.
- It explains its reasoning clearly.
- It adapts to multiple platforms (chats, games, comments).
- It grows ethically along with technology.

### A future-focused alignment

If we prioritize ethics and human values today, we can build a future where children can grow confidently alongside technology — not underneath its risks.

This isn’t just an AI agent.

It’s an argument for a new cultural approach to tech:
  **innovation and responsibility growing side by side.**

## Architecture

Agent Architecture: **Sequential Pipeline**

The system employs a SequentialAgent pipeline, which is deterministic, reliable, and mimics a specialized human analysis team. The output of one agent becomes the context (artifact) for the next, ensuring every stage is focused and efficient.

|S.No.|Agent Name|Role|Core Function|
|-----|----------|----|-------------|
|1.|Preprocessor Agent|Cleans text, tags context, detects language.|Normalizes noisy input and extracts metadata for the downstream classifier.|
|2.|Risk Classifier Agent|Determines primary risk category and confidence.|Uses Gemini to classify the message into one of six specific risk types.|
|3.|Risk Scorer Agent|Calculates final risk level using a custom tool.|Converts the LLM's subjective confidence score into an objective, policy-based LOW/MEDIUM/HIGH rating.|
|4.|Summary Agent|Generates the final, empathetic guardian report.|Formats the risk data into a three-part, supportive report for the parent/guardian.|

Below is the high-level structure of the agent.


                  ┌─────────────────────────────────────────┐
                  │         Data Sources (Inputs)           │
                  │─────────────────────────────────────────│
                  │  • Chat messages (DMs)                  │
                  │  • Gaming chat                          │
                  │  • Social media posts/comments          │
                  │  • Uploaded datasets (Kaggle)           │
                  └─────────────────────────────────────────┘
                                     │
                                     ▼
                      ┌────────────────────────────────┐
                      │  Preprocessing & Normalization │
                      │────────────────────────────────│
                      │  • Clean text                  │
                      │  • Remove noise / emojis       │
                      │  • Language detection          │
                      │  • Age-context tagging         │
                      └────────────────────────────────┘
                                     │
                                     ▼
             ┌────────────────────────────────────────────────────┐
             │        Safety Guardian Core (AI Agent)             │
             │────────────────────────────────────────────────────│
             │  1. Risk Classification                            │
             │     • Grooming                                     │
             │     • Bullying / Harassment                        │
             │     • Toxic / hateful language                     │
             │     • Manipulation / Coercion                      │
             │     • Explicit content                             │
             │                                                    │
             │  2. Risk Scoring                                   │
             │     • Low / Medium / High                          │
             │                                                    │
             │  3. Explanation Module                             │
             │     • Why the agent flagged it                     │
             │     • Which patterns were detected                 │
             └────────────────────────────────────────────────────┘
                                     │
                                     ▼
              ┌──────────────────────────────────────────────────┐
              │    Safety Actions Module (Optional Policy Layer) │
              │──────────────────────────────────────────────────│
              │  • Suggest blocking/reporting                    │
              │  • Recommend guidance for parents                │
              │  • Support “review only” mode (no interventions) │
              └──────────────────────────────────────────────────┘
                                     │
                                     ▼
         ┌─────────────────────────────────────────────────────────────┐
         │   Parent/Guardian Summary (Slightly Alert + Actionable)     │
         │─────────────────────────────────────────────────────────────│
         │  • Short safety report                                      │
         │  • Risk reasoning explained simply                          │
         │  • Recommended next steps                                   │
         │  • No fear-driven language                                  │
         └─────────────────────────────────────────────────────────────┘

## Key concepts demonstrated while building agent

**Technical Implementation**
The solution demonstrates expertise gained throughout the course by applying the following key concepts:

**1. Multi-agent system (Sequential Agents)**
**Implementation:** The agent is built using the `SequentialAgent` class from the ADK, orchestrating four specialized LLMAgent classes (`PreprocessorAgent`, `RiskClassifierAgent`, `RiskScorerAgent`, `SummaryAgent`).

**Value:** This modularity ensures high interpretability and debuggability. If the classification is wrong, we know exactly which agent (`RiskClassifierAgent`) needs instruction refinement, rather than debugging a single, monolithic prompt.

**2. Custom Tools for Policy Governance**
**Implementation:** The `RiskScorerAgent` is provided with the `calculate_risk_level` function tool. This tool takes the LLM's output (confidence_score: float) and applies a hard-coded business logic to return a policy-driven value (LOW, MEDIUM, or HIGH).

**Value:** This standardizes the final risk rating, removing the inherent subjectivity and potential variability of raw LLM output. It ensures the system's response aligns with pre-defined, non-negotiable safety policies, injecting auditability and governance into the generative process.

**3. Internal State Management (Context Flow)**
**Implementation:** The project utilizes the `output_key` parameter on each sub-agent (e.g., `output_key="preprocessed_data"`) to explicitly store structured data artifacts in the session state. The next agent's instruction then consumes this state via f-string referencing (e.g., `{preprocessed_data}`).

**Value:** This is critical for controlling the flow of context and data integrity. It guarantees that the Risk Classifier never receives raw, messy input, but only the cleaned, structured data produced by the Preprocessor, allowing each agent to operate on a consistent, verified state.

**4. Production Robustness**
**Implementation:** The underlying LLM model calls are configured with explicit types.HttpRetryOptions, specifying multiple retry attempts and specific HTTP status codes (429, 503, etc.) to retry on failure.

**Value:** This showcases adherence to production best practices, ensuring the agent remains resilient and operational under transient API errors or high-traffic conditions, thereby maximizing service availability.

### Ethical Considerations

- No personal data is stored.
- No surveillance; only user-provided text.
- Transparent risk scoring.
- No harmful or misleading predictions.
- Designed for guidance, not punishment.

### Value Statement

Shield-your-Tiny-Human is a dedicated multi-agent system that replaces poor and unreliable keyword-based safety tools and large monolithic LLM solutions with auditable and policy-based risk management system. 

The real value of the project is that we provide confidence and clarity by producing auditable safety reports from tangled, uncertain online interactions. 

