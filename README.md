# Awesome AgentOps

A curated list of open-source tools for running AI agents in production: evaluating them, tracing them,
keeping them inside their guardrails, and knowing what they cost.

Building an agent demo takes an afternoon. Keeping one reliable, safe and affordable once real users depend
on it is a different job, and this list is about that job. Open source first. Hosted products are only listed
when the core is open.

Contributions welcome. Read the [guidelines](CONTRIBUTING.md) first.

## Contents

- [Start here](#start-here)
- [Evaluation and testing](#evaluation-and-testing)
- [Tracing and observability](#tracing-and-observability)
- [Guardrails and runtime safety](#guardrails-and-runtime-safety)
- [Red-teaming and security testing](#red-teaming-and-security-testing)
- [Policy and authorisation](#policy-and-authorisation)
- [Gateways and cost control](#gateways-and-cost-control)
- [Tool integration (MCP and A2A)](#tool-integration-mcp-and-a2a)
- [Agent frameworks](#agent-frameworks)
- [Sandboxing and durable execution](#sandboxing-and-durable-execution)
- [Model serving](#model-serving)
- [Standards and guidance](#standards-and-guidance)

## Start here

If you're putting your first agent into production and want a small, sensible stack:

1. **Trace everything** with OpenTelemetry-based instrumentation ([OpenLLMetry](https://github.com/traceloop/openllmetry) or [OpenLIT](https://github.com/openlit/openlit)) into [Langfuse](https://github.com/langfuse/langfuse) or [Phoenix](https://github.com/Arize-ai/phoenix).
2. **Write a golden dataset** of 50-100 real cases and run it on every change with [promptfoo](https://github.com/promptfoo/promptfoo), [DeepEval](https://github.com/confident-ai/deepeval) or [Inspect](https://github.com/UKGovernmentBEIS/inspect_ai).
3. **Put a gateway in front of the models** ([LiteLLM](https://github.com/BerriAI/litellm)) so you get per-workflow cost tracking and can switch models without code changes.
4. **Check actions, not just prompts.** Scoped credentials plus a policy check ([OPA](https://github.com/open-policy-agent/opa)) before any tool call that writes.
5. **Attack it before users do** with [garak](https://github.com/NVIDIA/garak) or [PyRIT](https://github.com/Azure/PyRIT).

## Evaluation and testing

- [DeepEval](https://github.com/confident-ai/deepeval) - Pytest-style evaluation for LLM apps, with metrics for RAG, agents and tool use.
- [Inspect](https://github.com/UKGovernmentBEIS/inspect_ai) - Evaluation framework from the UK AI Security Institute. Strong on agentic and tool-using tasks.
- [promptfoo](https://github.com/promptfoo/promptfoo) - Declarative test cases for prompts, models and agents, with CI integration and red-teaming built in.
- [Ragas](https://github.com/explodinggradients/ragas) - Metrics and test-set generation for retrieval-augmented generation.
- [agentevals](https://github.com/langchain-ai/agentevals) - Evaluators for agent trajectories: did the agent take the right steps, not just reach the right answer.
- [openevals](https://github.com/langchain-ai/openevals) - Ready-made LLM-as-judge and structured-output evaluators.
- [OpenAI Evals](https://github.com/openai/evals) - Framework and registry of benchmarks for evaluating models and LLM systems.
- [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) - The standard harness for benchmarking language models on academic tasks.
- [HELM](https://github.com/stanford-crfm/helm) - Stanford's holistic evaluation framework for comparing models across many scenarios.
- [TruLens](https://github.com/truera/trulens) - Feedback functions and tracing for evaluating LLM apps and agents.
- [Giskard](https://github.com/Giskard-AI/giskard) - Automated scanning for quality, bias and security issues in LLM apps.

## Tracing and observability

- [Langfuse](https://github.com/langfuse/langfuse) - Tracing, prompt management, evaluations and cost tracking. Self-hostable.
- [Phoenix](https://github.com/Arize-ai/phoenix) - OpenTelemetry-native tracing and evaluation from Arize. Runs locally or self-hosted.
- [OpenLLMetry](https://github.com/traceloop/openllmetry) - OpenTelemetry instrumentation for LLM providers, vector DBs and agent frameworks.
- [OpenLIT](https://github.com/openlit/openlit) - OpenTelemetry-native observability for LLMs, GPUs and agents, with dashboards.
- [Opik](https://github.com/comet-ml/opik) - Tracing, evaluation and production monitoring from Comet.
- [Weave](https://github.com/wandb/weave) - Tracing and evaluation toolkit from Weights & Biases.
- [MLflow](https://github.com/mlflow/mlflow) - Long-standing ML platform with tracing and evaluation for GenAI apps.
- [Laminar](https://github.com/lmnr-ai/lmnr) - Open-source observability and evaluation platform focused on agents.
- [AgentOps](https://github.com/AgentOps-AI/agentops) - SDK for agent session replays, cost tracking and failure analysis.
- [Helicone](https://github.com/Helicone/helicone) - Proxy-based logging, cost tracking and caching for LLM requests.
- [Agenta](https://github.com/Agenta-AI/agenta) - Prompt playground, evaluation and observability in one platform.

If you already run an observability stack, the [OpenTelemetry Collector](https://github.com/open-telemetry/opentelemetry-collector) with [Jaeger](https://github.com/jaegertracing/jaeger) or [Tempo](https://github.com/grafana/tempo) can hold LLM traces too, following the [GenAI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/).

## Guardrails and runtime safety

- [NeMo Guardrails](https://github.com/NVIDIA/NeMo-Guardrails) - Programmable rails for dialogue flow, topics, jailbreak and fact checking.
- [Guardrails AI](https://github.com/guardrails-ai/guardrails) - Input and output validators, plus a hub of reusable checks.
- [LLM Guard](https://github.com/protectai/llm-guard) - Scanners for prompt injection, secrets, PII and toxic content.
- [Purple Llama](https://github.com/meta-llama/PurpleLlama) - Meta's safety tools, including Llama Guard classifiers and Prompt Guard.
- [Presidio](https://github.com/microsoft/presidio) - Detect and anonymise PII before it reaches a model or a log.
- [Invariant](https://github.com/invariantlabs-ai/invariant) - Rule-based guardrails and trace analysis for agent tool use.

## Red-teaming and security testing

- [garak](https://github.com/NVIDIA/garak) - LLM vulnerability scanner with a large library of probes.
- [PyRIT](https://github.com/Azure/PyRIT) - Microsoft's framework for automating red-team attacks on generative AI systems.
- [promptfoo red teaming](https://github.com/promptfoo/promptfoo) - Generates attacks tailored to your application and reports against OWASP and NIST categories.
- [prompt-injection-testbench](https://github.com/yashodhantek/prompt-injection-testbench) - Small CLI that runs canary- and marker-based injection attacks against an app or agent in CI. *(Disclosure: maintained by the author of this list.)*

## Policy and authorisation

Agents act through tools, so who-can-do-what belongs in policy, not in the prompt.

- [Open Policy Agent](https://github.com/open-policy-agent/opa) - General-purpose policy engine (Rego). A good fit for checking each tool call before it runs.
- [Cedar](https://github.com/cedar-policy/cedar) - Fast, analysable authorisation policy language from AWS.
- [Gatekeeper](https://github.com/open-policy-agent/gatekeeper) - OPA for Kubernetes admission control, useful when agents deploy or change infrastructure.

## Gateways and cost control

- [LiteLLM](https://github.com/BerriAI/litellm) - One OpenAI-compatible API for 100+ providers, with budgets, rate limits, fallbacks and spend tracking.
- [Portkey Gateway](https://github.com/Portkey-AI/gateway) - Lightweight AI gateway with routing, retries, caching and guardrail hooks.
- [agentgateway](https://github.com/agentgateway/agentgateway) - Proxy for agent traffic (MCP and A2A) with authentication, authorisation and observability.

## Tool integration (MCP and A2A)

- [Model Context Protocol](https://github.com/modelcontextprotocol/modelcontextprotocol) - The specification and docs for connecting agents to tools and data ([site](https://modelcontextprotocol.io)).
- [MCP reference servers](https://github.com/modelcontextprotocol/servers) - Official reference implementations, plus links to community servers.
- [MCP Inspector](https://github.com/modelcontextprotocol/inspector) - Visual tool for testing and debugging MCP servers.
- [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk) and [TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) - Official SDKs for building servers and clients.
- [A2A](https://github.com/a2aproject/A2A) - Agent2Agent protocol for agents built on different frameworks to talk to each other.

## Agent frameworks

Not exhaustive, just the ones you'll most often meet in production work. Pick one with good tracing hooks.

- [Google ADK](https://github.com/google/adk-python) - Agent Development Kit: multi-agent orchestration, tools and built-in evaluation.
- [LangGraph](https://github.com/langchain-ai/langgraph) - Stateful, graph-based agent workflows with checkpointing and human-in-the-loop.
- [Microsoft Agent Framework](https://github.com/microsoft/agent-framework) - Microsoft's framework for agents and multi-agent workflows in Python and .NET.
- [AutoGen](https://github.com/microsoft/autogen) - Multi-agent conversation framework. Microsoft now points new projects to Agent Framework.
- [CrewAI](https://github.com/crewAIInc/crewAI) - Role-based multi-agent crews and event-driven flows.
- [Pydantic AI](https://github.com/pydantic/pydantic-ai) - Type-safe agent framework from the Pydantic team.
- [OpenAI Agents SDK](https://github.com/openai/openai-agents-python) - Lightweight framework with handoffs, guardrails and tracing.
- [Claude Agent SDK](https://github.com/anthropics/claude-agent-sdk-python) - Anthropic's SDK for building agents on the same harness as Claude Code.

## Sandboxing and durable execution

- [E2B](https://github.com/e2b-dev/E2B) - Secure cloud sandboxes for running agent-generated code.
- [Temporal](https://github.com/temporalio/temporal) - Durable workflow engine. Useful when agent runs are long, need retries, or must survive restarts.

## Model serving

For running open-weight models inside your own network.

- [vLLM](https://github.com/vllm-project/vllm) - High-throughput inference server with an OpenAI-compatible API.
- [Ollama](https://github.com/ollama/ollama) - The easiest way to run models locally for development and testing.

## Standards and guidance

- [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/) - The most common security risks, with mitigations.
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) - A widely referenced framework for governing AI risk.
- [OpenTelemetry GenAI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/) - Standard attribute names for LLM and agent spans, so traces work across tools.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and related rights to this work.
