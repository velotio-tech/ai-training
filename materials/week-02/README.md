# Week 2: Multi-Agent Systems, Evaluation & Production

**Theme:** Multi-Agent & Production — Framework mastery, multi-agent patterns, evals, observability, responsible AI, capstone.

---

## Day 8: Agent Framework Landscape

**Learning Objectives**

- Compare major agent frameworks: LangGraph, CrewAI, OpenAI Agents SDK, Claude SDK, Google ADK, AWS Strands
- Understand framework selection criteria for different use cases
- Build hello-world agents in at least two frameworks

**Framework Comparison**

| Framework | Language | Orchestration Style | Key Strength | Best For |
|-----------|----------|---------------------|--------------|----------|
| LangGraph | Python/JS | Graph-based (cyclic) | Flexibility, checkpointing | Complex workflows, HITL |
| CrewAI | Python | Role-based crews | Ease of use, collaboration | Team-based agent tasks |
| OpenAI Agents SDK | Python | Handoff-based | Native OpenAI integration | OpenAI-centric stacks |
| Claude SDK | Python | Tool use + MCP | Extended thinking, safety | Anthropic-centric stacks |
| Google ADK | Python | Workflow agents | Gemini optimization | Google Cloud deployments |
| AWS Strands | Python | Model-driven | Production maturity | AWS deployments |

**Core Concepts**


| Concept            | Description                                                | Why it matters                                               |
| ------------------ | ---------------------------------------------------------- | -------------------------------------------------------------- |
| Agentic AI         | Workflows vs agents, autonomy control                      | Complex task execution |
| Orchestration        | State, memory, branching           | Real agent systems |


**Hands-On**

- Framework Exploration: "Hello world" agent in two frameworks; compare developer experience, docs, code verbosity.
- Feature Matrix: Comparison document for two frameworks — state management, tool calling, memory, streaming, deployment.

**Resources**

- LangGraph Quickstart — https://langchain-ai.github.io/langgraph/tutorials/introduction/
- CrewAI Documentation — https://docs.crewai.com/
- OpenAI Agents SDK — https://openai.github.io/openai-agents-python/
- Google ADK Overview — https://developers.googleblog.com/en/agent-development-kit-easy-to-build-multi-agent-applications/
- AWS Strands Introduction — https://aws.amazon.com/blogs/opensource/introducing-strands-agents-an-open-source-ai-agents-sdk/
- Anthropic MCP — https://modelcontextprotocol.io/
- Agentic AI - Building Effective Agents (Anthropic)](https://docs.anthropic.com/en/docs/building-effective-agents)

**Deliverable:** Comparison document with code samples from two frameworks.

---

## Day 9: Multi-Agent Architecture Patterns

**Learning Objectives**

- Master supervisor/orchestrator patterns
- Implement agents-as-tools delegation
- Understand swarm and peer-to-peer collaboration
- Design graph-based agent workflows

**Multi-Agent Patterns**

| Pattern | Structure | Communication | Best For |
|---------|-----------|---------------|----------|
| Supervisor | Central orchestrator delegates to workers | Top-down commands | Clear task delegation |
| Agents as Tools | Agents wrapped as callable tools | Function calls | Hierarchical expertise |
| Swarm | Autonomous agents with handoffs | Peer transfers | Flexible routing |
| Graph (LangGraph) | Nodes + edges with shared state | State passing | Complex workflows |
| Debate/Consensus | Agents critique each other | Multi-round discussion | Quality improvement |

**Hands-On**

- Supervisor System: Orchestrator that routes to two specialist agents (e.g. coding helper, research assistant).
- Agent Debate: Two agents debate a topic; judge agent determines winner.
- Swarm Handoff: Three agents that hand off using OpenAI Swarm patterns.

**Resources**

- Multi-Agent Architectures Benchmark — https://blog.langchain.com/benchmarking-multi-agent-architectures/
- OpenAI Swarm — https://github.com/openai/swarm
- Google A2A Protocol — https://a2a-protocol.org/
- CrewAI Multi-Agent — https://docs.crewai.com/concepts/crews
- LangGraph Multi-Agent — https://langchain-ai.github.io/langgraph/concepts/multi_agent/

**Deliverable:** Working multi-agent system with at least 3 agents (supervisor or swarm pattern).

---

## Day 10: Evaluation & Metrics for Agents

**Learning Objectives**

- Design evaluation datasets for agent testing
- Implement automated scoring with LLM-as-judge
- Measure tool correctness, task completion, reasoning quality
- Set up experiment tracking for prompt iterations

**EVALUATION = DATASET × TASK × SCORERS**

**Dataset Types**

| Type | Size | Purpose | Source |
|------|------|---------|--------|
| Golden Dataset | 50–200 cases | Core regression testing | Hand-curated |
| Edge Cases | 20–50 cases | Failure mode coverage | Bug reports, adversarial |
| Synthetic | 1000+ cases | Scale testing | LLM-generated |
| Production Samples | Ongoing | Real-world validation | User queries |

**Key Metrics**

| Metric | What It Measures | How to Calculate |
|--------|------------------|------------------|
| Task Completion Rate | End-to-end success | Completed tasks / Total attempts |
| Tool Correctness | Correct tool selection | Correctly used tools / Total tool calls |
| Reasoning Quality | Logic coherence | LLM-as-judge (1–5 scale) |
| Faithfulness | Grounded in sources | FACTSCORE or semantic similarity |
| Latency | Response time | P50, P95 |
| Cost Efficiency | Token usage | Cost per successful task |

**Hands-On**

- Golden Dataset Creation: 20-case test dataset for Week 1 agent (happy paths + edge cases).
- Automated Evaluation Pipeline: LLM-as-judge scoring; track scores across prompt iterations.
- DeepEval Integration: Automated evaluations with built-in metrics.

**Resources**

- DeepEval Metrics Introduction — https://deepeval.com/docs/metrics-introduction
- Braintrust Evaluation Guide — https://www.braintrust.dev/docs/guides/evals
- LangSmith Evaluation — https://docs.smith.langchain.com/evaluation
- LLM-as-Judge Best Practices — https://arxiv.org/abs/2306.05685
- Prompt/model regressions - [LangSmith](https://docs.smith.langchain.com/)

**Deliverable:** Evaluation pipeline with 20+ test cases and automated LLM-as-judge scoring.

---

## Day 11: Observability & Production Debugging

**Learning Objectives**

- Implement comprehensive tracing for agent systems
- Set up cost and latency monitoring dashboards
- Master production debugging workflows
- Configure prompt versioning and A/B testing

**Observability Stack**

- Application Layer: Agent code with instrumentation
- Collection Layer: OpenTelemetry / Native SDK
- Platform Layer: Langfuse, LangSmith, Braintrust, Phoenix
- Analysis Layer: Trace exploration, cost analytics, latency dashboards, error tracking

**Key Patterns**

| Pattern | Purpose | Implementation |
|---------|---------|----------------|
| Trace Spans | Track request lifecycle | Wrap each component (LLM, tool, retrieval) |
| Cost Attribution | Budget management | Log tokens per request, aggregate by feature |
| Latency Tracking | Performance SLAs | TTFT, total completion time, P50/P95 |
| Error Correlation | Root cause analysis | Link errors to prompts/inputs |
| Prompt Versioning | Rollback capability | Tag each prompt with version ID |

**Hands-On**

- Langfuse Setup: Instrument multi-agent system; capture traces for 20+ interactions.
- Cost Dashboard: Cost per agent, cost per tool, total daily spend.
- Debug Session: Introduce a bug; use traces to find and fix it.

**Resources**

- Langfuse Quickstart — https://langfuse.com/docs/get-started
- LangSmith Tracing — https://docs.smith.langchain.com/tracing
- Phoenix OTel Integration — https://docs.arize.com/phoenix
- OpenLLMetry — https://github.com/traceloop/openllmetry
- Production LLM Monitoring — https://www.honeycomb.io/llm-observability
- LLMOps - [OpenAI Production Best Practices](https://platform.openai.com/docs/guides/production-best-practices)

**Deliverable:** Fully instrumented agent with Langfuse traces and cost tracking report.

---

## Day 12: Responsible AI & Guardrails

**Learning Objectives**

- Implement input/output guardrails for agent safety
- Defend against prompt injection attacks
- Design content moderation pipelines
- Understand compliance requirements for AI systems

**Guardrail Types**

| Type | Purpose | Tools |
|------|---------|--------|
| Input Validation | Block malicious inputs | NeMo Guardrails, Guardrails AI |
| Prompt Injection Defense | Prevent instruction override | Input classification, XML tag separation |
| Content Moderation | Filter harmful outputs | OpenAI Moderation API, Perspective API |
| PII Protection | Mask sensitive data | Presidio, regex patterns |
| Factuality Check | Reduce hallucinations | RAG grounding, citation verification |

**Hands-On**

- Injection Attack Lab: Try 10 prompt injection techniques; document which succeed; implement defenses.
- Guardrails Implementation: NeMo Guardrails or Guardrails AI with at least 3 rules (topic restriction, PII masking, output validation).
- Red Team Session: promptfoo automated red-teaming; fix vulnerabilities.

**Resources**

- OWASP LLM Top 10 — https://owasp.org/www-project-top-10-for-large-language-model-applications/
- NeMo Guardrails — https://docs.nvidia.com/nemo/guardrails/
- Guardrails AI — https://www.guardrailsai.com/docs
- promptfoo Red Teaming — https://www.promptfoo.dev/docs/red-team/
- Anthropic Constitutional Classifiers — https://www.anthropic.com/news/constitutional-classifiers
- Security & governance - [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- Risk management - [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- Deployment & rollout (Safe launches) - OpenAI Production Best Practices](https://platform.openai.com/docs/guides/production-best-practices)

**Deliverable:** Agent with guardrails passing a 10-case adversarial test suite.

---

