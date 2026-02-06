# RepKit — A Reputation SDK for [AI Agents](https://reputagent.com)

> **Status: Work in Progress** — [Star this repo](https://github.com/ReputAgent/repkit) to get notified when we ship.

[RepKit](https://reputagent.com/repkit) turns every [agent interaction](https://reputagent.com/glossary/agent-communication) into an [evaluation](https://reputagent.com/glossary/evaluation) event. When Agent A delegates to Agent B, Agent A observes the outcome. That observation becomes data. Accumulated data becomes [reputation](https://reputagent.com/glossary/reputation).

Because [a benchmark is a snapshot — reputation is a trajectory](https://reputagent.com/about).

**[Full product overview at reputagent.com/repkit](https://reputagent.com/repkit)**

## The Problem

[Over 40% of agentic AI projects will be canceled by 2027](https://reputagent.com/about) (Gartner). Teams can't answer a simple question: *"Can I trust this agent?"*

Benchmarks measure capability at one moment. They don't tell you if an agent is consistent, how it handles [edge cases](https://reputagent.com/failures), or whether it's [improving over time](https://reputagent.com/glossary/drift).

RepKit makes [continuous evaluation](https://reputagent.com/patterns) operational infrastructure — not a gate before deployment, but a system that runs during production.

## How It Works

```
Interaction → Evaluation → Accumulation → Reputation
```

1. **Interaction** — Agent A delegates a task to Agent B
2. **Evaluation** — Agent A observes the outcome and logs it via RepKit
3. **Accumulation** — Evaluations aggregate across interactions and time
4. **Reputation** — [Trust signals](https://reputagent.com/glossary/trust-signal) power routing, access, and governance decisions

## API Preview

```python
from repkit import RepKit

rk = RepKit(api_key="rk_...")

# Log an evaluation from an agent-to-agent interaction
rk.log_interaction_evaluation(
    interaction_id="txn-789",
    agent="agent-123",
    dimensions={
        "accuracy": 0.95,
        "safety": 0.88,
        "helpfulness": 0.93
    }
)

# Query reputation — accumulated from all evaluations
rep = rk.get_reputation("agent-123")
print(rep.score)        # 7.8
print(rep.trend)        # "improving"
print(rep.eval_count)   # 142
```

```typescript
import { RepKit } from "@reputagent/repkit";

const rk = new RepKit({ apiKey: "rk_..." });

await rk.logEvaluation({
  interactionId: "txn-789",
  agent: "agent-123",
  dimensions: { accuracy: 0.95, safety: 0.88, helpfulness: 0.93 },
});

const rep = await rk.getReputation("agent-123");
```

## What Reputation Powers

| Use Case | How Reputation Helps |
|----------|---------------------|
| **[Routing](https://reputagent.com/glossary/routing)** | Which agent gets this task? Route based on track record. |
| **[Access control](https://reputagent.com/glossary/access-control)** | What capabilities unlock? Permissions earned through reliability. |
| **[Delegation](https://reputagent.com/glossary/delegation)** | Should A trust B's output? Historical evidence decides. |
| **[Governance](https://reputagent.com/glossary/ai-governance)** | What oversight level? Tiered autonomy based on [trust signals](https://reputagent.com/glossary/trust-signal). |

## Design Principles

- **Evidence over assertions** — RepKit aggregates structured [evaluation](https://reputagent.com/glossary/evaluation) inputs over time, not single-run judgments
- **Reputation over scores** — Signals accumulate across interactions and versions, producing durable reputation
- **Signals, not decisions** — RepKit computes reputation signals; enforcement remains under your control

## What RepKit Does Not Do

RepKit records evaluations, computes reputation, and exposes results via API. It does not:
- Mandate a specific judge model or evaluator
- Require a routing framework or agent runtime
- Enforce decisions — you remain in control

## Built on Documented Patterns

RepKit implements concepts from the [ReputAgent evaluation patterns library](https://reputagent.com/patterns):

- **[LLM-as-Judge](https://reputagent.com/patterns/llm-as-judge-pattern)** — Automated evaluation using language models
- **[Human-in-the-Loop](https://reputagent.com/patterns/human-in-the-loop-pattern)** — Human oversight for high-stakes decisions
- **[Reflection Pattern](https://reputagent.com/patterns/reflection-pattern)** — Agents that evaluate their own outputs
- **[Red Teaming](https://reputagent.com/patterns/red-teaming-pattern)** — Adversarial testing for robustness

Avoids documented [failure modes](https://reputagent.com/failures):
- **[Sycophancy Amplification](https://reputagent.com/failures/sycophancy-amplification)** — Agents that agree rather than evaluate honestly
- **[Hallucination Propagation](https://reputagent.com/failures/hallucination-propagation)** — Errors that cascade through agent chains
- **[Mutual Validation Trap](https://reputagent.com/failures/mutual-validation-trap)** — Agents that validate each other's mistakes

## Related

- **[reputagent-data](https://github.com/ReputAgent/reputagent-data)** — Open dataset of 404 entries: [failure modes](https://reputagent.com/failures), [evaluation patterns](https://reputagent.com/patterns), [use cases](https://reputagent.com/use-cases), [glossary](https://reputagent.com/glossary), [ecosystem tools](https://reputagent.com/ecosystem), and [research index](https://reputagent.com/research)
- **[Agent Playground](https://reputagent.com/playground)** — Pre-production testing where agents build track record through real [multi-agent scenarios](https://reputagent.com/use-cases)
- **[ReputAgent](https://reputagent.com)** — The full platform for [agent reputation and evaluation](https://reputagent.com/about)

## Get Early Access

RepKit is in development. [Request early access at reputagent.com/repkit](https://reputagent.com/repkit#early-access).

## License

Apache-2.0 — see [LICENSE](LICENSE).

---

*Patent pending. RepKit represents one embodiment of the claimed inventions. Descriptions here are illustrative and do not limit the scope of current or future claims.*
