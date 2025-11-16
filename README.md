# Shield-your-Tiny-Human

A multi-agent AI system for the detection of online risks for children in chats, comments, and other social spaces with the intention of helping families stay safe by precaution-as technology is growing faster day by day.

Technology today is sprinting at a pace that feels almost unreal. Every morning, something new drops — smarter AI, faster algorithms, hyper-personalized feeds, immersive digital worlds. Kids and teens are stepping into this rapidly evolving space long before most adults ever get a chance to understand it. And while this growth is exciting, it creates a very real imbalance: tech evolves daily, but safeguards don’t.
**That gap is exactly where the “Child Online Safety Guardian” lives.**

This project explores how AI can act as a gentle but firm shield for kids and teens across digital platforms — chats, gaming lobbies, DMs, comment sections, and social spaces — detecting threats, inappropriate content, manipulation, grooming patterns, toxic language, cyberbullying, and hidden online risks.

Here is the core philosophy behind the project:

>**Technology will always grow — faster than we expect, faster than we can control. But our responsibility grows with it. If we care enough to build systems that think about child safety, fairness, and balance at every step, then innovation and protection can move forward together. Tech doesn’t have to leave humanity behind — we can choose to build tools that hold both progress and ethics in the same hand.**

<img width="700" height="600" alt="ChatGPT Image Jun 27, 2116, 03_56_49 PM" src="https://github.com/user-attachments/assets/f12eac5d-c02f-4537-8bba-2d8579575c5c" />



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

If we prioritize ethics and human values today, we can build a future where children grow confidently alongside technology — not underneath its risks.

This isn’t just an AI agent.

It’s an argument for a new cultural approach to tech:
  **innovation and responsibility growing side by side.**

## Architecture

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

This project includes more than three required course concepts:

1. Multi-agent system
   - Preprocessor agent
   - LLM-based risk classifier
   - Safety scoring agent
   - Action guidance agent
   - Optional memory agent
2. Tooling
   - Code execution tools
   - Custom classification tools
3. Long-running operations
   - Pause/resume analysis
   - Stream-based message processing
4. Sessions & Memory
   - Per-child session
   - Multi-turn context
   - Cumulative risk summaries
5. Observability
   - Logging
   - Decision trace
   - Agent metrics
6. Deployment-ready architecture (Optional)
   - Can run as a Kaggle Notebook or API service
   - Includes modular functions

### Ethical Considerations

- No personal data is stored.
- No surveillance; only user-provided text.
- Transparent risk scoring.
- No harmful or misleading predictions.
- Designed for guidance, not punishment.

