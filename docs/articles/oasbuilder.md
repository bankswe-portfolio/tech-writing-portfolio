# OASBuilder and Automation-Ready API Documentation

API documentation is still often written for humans first, even when downstream systems need machine-readable specifications to use those same interfaces. A 2025 ACL Industry paper from IBM Research looks directly at that gap with OASBuilder, a system that "transforms long and diverse API documentation pages into consistent, machine-readable API specifications."

The problem setup is practical. Many providers publish HTML documentation instead of OpenAPI specs, which leaves external users manually converting long, inconsistent pages into OAS before those APIs can be used in automation workflows. OASBuilder addresses that with a staged pipeline: it segments a documentation page by operation, extracts demonstrative and descriptive evidence, generates partial OAS in parallel, merges them, and then enriches missing metadata. As the authors put it, "The generation task is divided into smaller sub-tasks, whose outputs are then combined to create a cohesive result."

That design choice is what makes the paper useful. It treats documentation conversion as a workflow problem rather than a prompting trick. The system uses domain knowledge about how API docs are structured, constrains what each LLM call has to do, and preserves a manual validation layer tied back to the source page.

The evaluation also goes beyond simple syntactic validity. On 50 webpages covering 189 operations, the best model produced valid OAS for 89% of cases. In semantic evaluation on 108 operations containing thousands of parameters and properties, request-side precision reached 0.96 and recall 0.86. Response recall was lower, which the authors attribute to deeply nested response structures and the frequent lack of descriptive documentation for response properties.

For technical writers, the implication is broader than API spec generation alone. Documentation quality now affects whether systems can derive usable machine-readable specifications from the docs themselves. Completeness, examples, parameter descriptions, and structural consistency are no longer only readability concerns. They shape whether documentation can participate directly in automation.

The enterprise result is also telling. OASBuilder has already been deployed, "saving thousands of hours of manual effort and making hundreds of complex enterprise APIs accessible as tools for LLMs."

For teams working on SDKs, APIs, and integration-heavy platforms, this pushes documentation closer to automation-ready infrastructure. Less effort goes into hand-transcribing interface structure. More effort goes into making source docs clear, complete, and grounded enough for downstream systems to use.

## Source

- Lazar et al., ACL Industry 2025
