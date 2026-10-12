# Artyom / spbstyle
**Applied AI Engineer** / Systems, Sandboxing & Agent Orchestration  
[Email](spbstyledev@gmail.com) · [Telegram](https://t.me/fiatow)

---

### Overview

Software engineer specializing in the intersection of non-deterministic systems and deterministic backend infrastructure. 

My work focuses on:
- Designing stateful, cyclic agent architectures with checkpointed persistence.
- Safe execution environments for untrusted, model-generated code (SAST + OS-level isolation).
- Quantitative system evaluation to measure agentic self-healing, pass rates, and security boundaries.

---

### Selected Architecture

#### [Arbitra](https://github.com/spbstyle/arbitra) — Autonomous Secure Code Generation Engine
An asynchronous distributed system designed for automated Python code synthesis, multi-layer validation, and sandboxed test execution.

* **Decoupled Architecture:** Event-driven backend built with FastAPI, Taskiq, and Redis, separating heavy LLM generation tasks and container operations from the core API layer.
* **Stateful Graph Orchestration:** LangGraph-based state machine with AST parsing, pre-execution SAST auditing via Semgrep, automated test generation, and an iterative self-healing loop driven by parsed runtime tracebacks.
* **Security & Isolation:** Ephemeral Docker containers strictly isolated at the OS level (`--network none`, 256MB RAM, restricted CPU quotas, PID exhaustion limits). Implements a stateful Human-in-the-Loop gate for pre-execution code inspection.
* **Empirical Validation:**
  - **OpenAI HumanEval:** Reached **100.0% Pass@Final** with a verified **+10.0% lift** produced entirely by the automated reflection/repair cycle.
  - **Adversarial Security Suite:** Achieved a **100% interception and remediation rate** across CWE-95 (Code Injection), CWE-78 (Command Injection), and CWE-502 (Deserialization).

---

### Technical Focus

* **Agent Orchestration & State Management:**  
  LangGraph, state checkpointing (`AsyncPostgresSaver`), cyclic error-recovery loops, asynchronous interrupt/resume flows (HITL).

* **Runtime Isolation & Security:**  
  Air-gapped execution environments, static application security testing (Semgrep), AST-level syntax and dependency inspection.

* **LLM Evaluation & Benchmarking:**  
  Evaluation harnesses, Pass@k metrics, regression testing against standard datasets and adversarial prompts.

* **Backend & Distributed Systems:**  
  Python (AsyncIO), FastAPI, Taskiq, Redis, PostgreSQL 16 (SQLAlchemy 2.0), Docker Compose.

---

### Engineering Approach

1. **Deterministic Verification over Blind Trust:** Model outputs are treated as untrusted user input. Code is statically analyzed and executed within isolated environments before acceptance.
2. **Quantified Iteration:** Architectural changes must be supported by measurable delta in task completion rates, repair accuracy, or latency benchmarks.
3. **Resilient Persistence:** Transient agent states are checkpointed to handle infrastructure failure and allow human intervention without losing context.
