# Documentation-to-Code Traceability with LLMs

Traceability has been a persistent challenge in software engineering.

Docs and code evolve at different speeds. When links between them break, impact analysis, refactoring, and even onboarding become harder than they need to be.

A recent 2025 study, *Evaluating the Use of LLMs for Documentation to Code Traceability*, provides one of the most systematic examinations I have seen of whether large language models can help with doc-to-code traceability.

The authors define the problem clearly:

> "Documentation-to-code traceability focuses on linking natural language documentation to the corresponding code implementations."

To evaluate this, they built two new datasets from modern open-source projects created after model training cutoffs. They tested Claude 3.5 Sonnet, GPT-4o, and o3-mini against traditional baselines including TF-IDF, BM25, and CodeBERT.

On raw link identification, the results are concrete:

> "We find that the best-performing LLM achieves F1-scores of 79.4% and 80.4% … substantially outperforming our baselines (whose best F1-scores were 54.2% and 69.3%, respectively)."

Precision across LLMs exceeded 87 percent. Recall varied more substantially. High precision suggests LLM-proposed links are often valid. Lower recall means links can still be missed, particularly at higher abstraction levels.

The paper also evaluates whether models can explain relationships and reconstruct multi-step trace chains. On explanation quality, the authors report:

> "We find that while fully correct relationship explanations range from 42.9% to 71.1%, partial accuracy exceeds 97%, indicating that fundamental connections are rarely missed."

Even when explanations are incomplete, the core relationship is usually identified correctly.

For technical writers, this is directly relevant.

First, traceability becomes something measurable within a documentation workflow. If a segment can be evaluated against candidate artifacts in a controlled way, trace validation becomes repeatable rather than manual.

Second, the error analysis is instructive. False positives often stem from naming assumptions or architectural pattern bias. Those failure modes mirror risks writers already manage when reviewing generated diagrams or API summaries.

Third, task framing matters. A one-to-many matching strategy consistently outperformed a many-to-many approach. Workflow design influences documentation accuracy as much as model choice.

Practically, LLMs can act as high-precision trace discovery assistants when paired with structured prompts and human review. They reduce search space and surface candidate relationships. Writers still interpret intent and meaning.

If documentation is expected to live inside CI pipelines and evolve with code, traceability cannot remain informal. This paper provides data for how that shift might look in practice.

## Source

- *Evaluating the Use of LLMs for Documentation to Code Traceability*
