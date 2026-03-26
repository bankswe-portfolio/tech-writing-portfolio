# OASBuilder and Automation-Ready API Documentation

> API documentation is becoming relevant not only as human guidance, but as a source for machine-readable interfaces and downstream automation.

**Type:** Article  
**Audience:** Technical writers, developer docs teams, API/platform teams  
**Theme:** API docs, automation, documentation as infrastructure

## Why this matters

Many providers publish HTML documentation instead of OpenAPI specifications. That leaves developers or platform teams manually converting long, inconsistent pages into machine-readable API specs before those APIs can be used in automation workflows.

A 2025 ACL Industry paper from IBM Research examines that gap with **OASBuilder**, a system designed to transform long, varied API documentation pages into consistent machine-readable API specifications.

## What changes

The design is what makes the paper useful. OASBuilder treats documentation conversion as a workflow problem rather than a prompting trick.

It segments a documentation page by operation, extracts both descriptive and demonstrative evidence, generates partial OAS in parallel, merges the results, and then enriches missing metadata. That staged structure matters because it constrains what each LLM call has to do. Instead of asking a model to infer an entire interface from a long HTML page at once, it narrows the task into smaller, interpretable steps with a validation layer tied back to the source page.

The evaluation also goes beyond syntactic validity. On 50 webpages covering 189 operations, the best model produced valid OAS for 89 percent of cases. In semantic evaluation on 108 operations containing thousands of parameters and properties, request-side precision reached 0.96 and recall 0.86. Response recall was lower, which the authors attribute to deeply nested response structures and the frequent lack of descriptive documentation for response properties.

## Implications for technical writing

The broader implication is that documentation quality now affects whether systems can derive usable machine-readable specifications from the docs themselves. Completeness, examples, parameter descriptions, and structural consistency are no longer only readability concerns. They shape whether documentation can participate directly in automation.

For teams working on SDKs, APIs, and integration-heavy platforms, this pushes documentation closer to automation-ready infrastructure. Less effort goes into hand-transcribing interface structure. More effort goes into making source docs clear, complete, and grounded enough for downstream systems to use.

## Source

- Lazar et al., ACL Industry 2025
