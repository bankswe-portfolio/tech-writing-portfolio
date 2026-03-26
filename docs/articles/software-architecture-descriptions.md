# Regenerating Software Architecture Descriptions

Architecture docs tend to drift for a familiar reason: systems evolve continuously, while architecture descriptions are usually updated manually and infrequently.

A 2025 paper by Hatahet, Knieke, and Rausch looks at this problem from a different angle. Instead of asking how to write better architecture docs, it asks whether architecture descriptions can be derived from the implementation itself.

The authors focus on Software Architecture Descriptions (SADs), which they note are often "missing, incomplete, or partially or severely outdated." When that happens, teams fall back to reading source code directly, even though "source code inherently lacks the necessary architectural abstraction and is thus not suited for broad stakeholder comprehension."

Their proposed solution is deliberately constrained. They combine reverse engineering with an LLM, but the LLM is not asked to infer architecture from raw code.

The pipeline works in stages. First, reverse engineering extracts a structural representation of the system. This produces a class-level view that is accurate but noisy. The LLM is then used to abstract that representation by identifying what the authors call "architecturally significant elements (core components)."

As they state, the goal is to generate "a dual-view SAD: 1) an abstract component diagram capturing the system's structure and 2) a set of state machine diagrams illustrating key component behaviors."

The paper is clear about why this division matters. Reverse engineering provides factual grounding. The LLM performs abstraction and summarization on structured inputs, rather than inventing architecture from scratch. This keeps the model's role interpretive rather than authoritative.

The evaluation results are mixed in an instructive way. The approach works well for smaller and moderately complex components. For larger components, especially when behavioral logic becomes intricate, the generated diagrams show gaps and inconsistencies. The authors note that "domain-specific examples notably improved behavioral modeling," while generic prompts performed poorly.

That limitation is part of what makes this work useful. It treats architecture docs as a system artifact with observable failure modes, not as a narrative that is either correct or incorrect by intent alone.

For technical writers working on SDKs, platforms, and complex systems, the implication is not that architecture docs can be fully automated. It is that baseline architecture descriptions can be regenerated from implementation artifacts, while human effort shifts toward explaining intent, tradeoffs, and design rationale that are not present in the code.

Related research is starting to explore what happens next, including how generated architecture diagrams can remain aligned as systems continue to change. While this paper focuses on generation, keeping those artifacts living over time is the obvious follow-on question.

## Source

- Hatahet, Knieke, and Rausch, 2025
