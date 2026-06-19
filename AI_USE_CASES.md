# AI Use Cases (2026) — Sprint Planner

## Agentic upgrade — 4-role CrewAI crew
- **PM agent** — pulls JD/Linear/Jira backlog via MCP, prioritises
- **Scrum Master** — capacity model, leave-aware
- **Architect** — flags stories needing design spike
- **Engineer** — story-point calibration from historical velocity (RAG over past sprints)

## Stack (free/OSS)
- **Crew:** CrewAI, AutoGen, LangGraph
- **MCP:** Jira, Linear, GitHub Projects
- **LLMs:** Claude Sonnet 4.6 (calibration), Gemini long-context (risk forecast with full sprint history)
- **Eval:** Promptfoo — measure calibration MAE vs actual story-completion data
- **Observability:** Langfuse — log every story-point suggestion + outcome

## Prompt pattern (calibration)
```
Given historical sprints {history} and proposed story "{title}",
return a single integer story-point estimate using Fibonacci (1,2,3,5,8,13,21,34).
Cite the 2 most-similar historical stories as evidence.
If similar stories had widely different outcomes, return a range and recommend a spike.
```

## Eval (Promptfoo)
- Golden set: 50 past sprints with actual hours-to-complete per story
- Metric: Mean Absolute Error on story-point predictions
- Pass: MAE ≤ 5 SP across the set

## Limitations
Jira/Linear MCP requires OAuth. Historical velocity is mocked in this prototype.
